************************************************************************************************************************
发布角色卡
************************************************************************************************************************

在发布角色卡前, 你需要去掉角色卡中的 ``http://localhost:5500/...`` 完全复制粘贴为其实际 .html 或 .js 文件里的内容.

.. warning::

  千万千万千万不要直接复制 .ts 文件到角色卡中.

.. note::

  当然也许你可以将脚本直接传到 catmoe 之类的地方, 然后用那个地址?

例如,

.. tabs::

  .. tab:: 编写时

    .. code-block:: html

      <script src="http://localhost:5500/build/src/脚本名.js"></script>

  .. tab:: 发布角色卡时

    .. code-block:: html

      <script>
      function detectMessageEdited(message_id: string) {
        alert(`你刚刚修改了第 ${message_id} 条聊天消息对吧😡`);
      }
      tavernOn(tavern_events.MESSAGE_EDITED, detectMessageEdited);
      </script>

在替换好后, 你就能正常发布角色卡.