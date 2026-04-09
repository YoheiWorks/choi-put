# SvelteファイルがコンパイルされずにNode.jsに渡される

## 何をやったか？

- shadcn-svelte#sidebarの`Your First Sidebar`サンプルコードをコピペした
- [https://www.shadcn-svelte.com/docs/components/sidebar]

## ブラウザのエラー

```text
Unknown file extension ".svelte" for /Users/enmore-yohei/sveltekit/choi-put/node_modules/bits-ui/dist/bits/accordion/components/accordion.svelte

TypeError [ERR_UNKNOWN_FILE_EXTENSION]: Unknown file extension ".svelte" for /Users/enmore-yohei/sveltekit/choi-put/node_modules/bits-ui/dist/bits/accordion/components/accordion.svelte

at Object.getFileProtocolModuleFormat [as file:] (node:internal/modules/esm/get_format:185:9)

at defaultGetFormat (node:internal/modules/esm/get_format:211:36)

at defaultLoad (node:internal/modules/esm/load:94:16)

at nextLoad (node:internal/modules/esm/hooks:785:28)

at AsyncLoaderHooksOnLoaderHookWorker.load (node:internal/modules/esm/hooks:410:26)

at MessagePort.handleMessage (node:internal/modules/esm/worker:251:24)

at [nodejs.internal.kHybridDispatch] (node:internal/event_target:843:20)

at MessagePort.<anonymous> (node:internal/per_context/messageport:23:28)
```

## 原因

Svelte 5（および最新のSvelteKit）と bits-ui（shadcn-svelteの土台）の組み合わせで、SSR（サーバーサイドレンダリング）時に時々発生する「SvelteファイルがコンパイルされずにNode.jsに渡されちゃう」という典型的なトラブルです。

原因は、Node.jsが .svelte という拡張子をどう扱えばいいか分からず、エラーを吐いていることにあります。本来はViteがそれをJavaScriptに変換すべきなのですが、node_modules 内のライブラリだとその処理がスキップされてしまうことがあるんです。

## 解決策

1. vite.config.ts の修正
    vite.config.ts を開き、ssr オプションを追加（または修正）する

    ```vite.config.ts
        import { sveltekit } from '@sveltejs/kit/vite';
        import { defineConfig } from 'vite';

        export default defineConfig({
            plugins: [sveltekit()],
            // ここから追加
            ssr: {
                noExternal: ['bits-ui']
            }
            // ここまで
        });
    ```

## なぜこれで治るのか？

- noExternal: ここにライブラリ名を指定すると、Viteはそのライブラリを「外部（External）のNode.jsパッケージ」として扱うのではなく、プロジェクトのソースコードと同じように「Viteのコンパイラ」を通して処理してくれます。これにより、.svelte ファイルが正しくJSに変換されるようになります。
