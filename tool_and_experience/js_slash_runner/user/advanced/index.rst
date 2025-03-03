************************************************************************************************************************
进阶: 分文件编写脚本
************************************************************************************************************************

你当然可以利用 module 进行分文件编写:

.. code-block:: typescript
  :linenos:
  :caption: ``src/index.ts``

  import { detectMessageUpdated } from './util.js'  // 注意是 .js

.. code-block:: typescript
  :linenos:
  :caption: ``src/util.ts``

  export function detectMessageUpdated(message_id: number) {
    alert(`你刚刚修改了第 ${message_id} 条聊天消息对吧😡`);
  }

========================================================================================================================
实时修改脚本内容
========================================================================================================================

你只需要按之前单文件那样使用入口文件即可; 但相比于之前的写法, 你需要在 ``<scripdoc>`` 中指定类型为 module:

.. code-block:: html

  <script type="module" src="http://localhost:5500/build/src/index.js"></script>

========================================================================================================================
打包为单文件
========================================================================================================================

在编写完成后, 你可以用 rollup 将结果打包为单个文件.

首先安装 rollup 和 @rollup/plugin-typescript:

.. code-block:: bash

  npm i -g rollup @rollup/plugin-typescript path url

然后编写 rollup.config.js 来配置要如何打包. 一般而言, 按下面的配置即可:

.. code-block:: javascript
  :linenos:
  :emphasize-lines: 7-10

  import typescript from '@rollup/plugin-typescript';
  import path from 'path'
  import { fileURLToPath } from 'url';

  export default {
    input: Object.fromEntries(
      [
        'src/角色卡1/index.ts',  // 填入你某张角色卡脚本的入口文件
        'src/角色卡2/index.ts',
      ].map(file => [
        file.slice(0, file.length - path.extname(file).length),
        fileURLToPath(new URL(file, import.meta.url)),
      ]),
    ),
    output: {
      dir: 'dist',
      format: 'es',
    },
    plugins: [typescript()],
  };


然后我们在该目录下运行 ``rollup -c`` 即可将其打包.

========================================================================================================================
第三方库
========================================================================================================================

你仍然可以用 :doc:`cdnjs, ESM>CDN 等提供的第三方库 </tool_and_experience/js_slash_runner/user/resource/index>`:

.. code-block:: typescript

  import 'https://cdnjs.cloudflare.com/ajax/libs/yamljs/0.3.0/yaml.min.js'
  import YAML from 'https://esm.sh/yaml'