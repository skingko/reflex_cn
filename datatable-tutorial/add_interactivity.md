# 为数据表添加互动性

现在我们将为数据表添加互动性。我们可以通过事件处理器和事件触发器来实现。

第一个例子实现了一个 `on_cell_clicked` 事件触发器的处理器，当用户点击数据编辑器中的单元格时，将触发该事件。事件触发器接收到单元格的坐标。

状态中有一个名为 `clicked_cell` 的变量，它将存储有关点击了哪个单元格的消息。我们定义了一个事件处理器 `get_clicked_data`，当它被调用时，它会更新 `clicked_cell` 变量的值。实质上，我们点击了一个单元格，调用了 `on_cell_clicked` 事件触发器，该触发器又调用了 `get_clicked_data` 事件处理器，该处理器更新了 `clicked_cell` 变量。

`on_cell_context_menu` 事件处理器的用法与 `on_cell_clicked` 相同，只是在用户右键点击时调用，即单元格应该显示上下文菜单时才调用。

## 编辑单元格

我们将展示另一种重要的互动方式，即如何编辑单元格。在这里，我们使用 `on_cell_edited` 事件触发器根据用户输入来更新数据。

`on_cell_edited` 事件触发器在用户修改单元格内容时被调用。它接收到单元格的坐标和修改后的内容。我们将它们传递给 `get_edited_data` 事件处理器，并用它们来更新相应位置的 `data` 状态变量。然后，我们更新 `edited_cell` 变量的值。

我们可以在 `columns` 中定义组标题，这些标题包含一组列。我们在 `columns` 中使用类似 `"group": "Data"` 的 `group` 属性来定义它们。`columns` 的定义如下所示。只有 `Title` 不属于组标题，其余都属于 `Data` 组标题。

现在，表格的标题如下所示。

我们可以对组标题应用几个事件触发器。

在这个例子中，我们使用 `on_group_header_context_menu` 事件触发器，当用户右键点击组标题时调用它。它返回组标题的 `index` 和 `data`。我们还可以使用 `on_group_header_clicked` 和 `on_group_header_renamed` 事件触发器，它们分别在用户左键点击组标题和用户重命名组标题时被调用。

还有几个值得探索的其他事件触发器。`on_item_hovered` 事件触发器在用户悬停在数据表中的某个项目上时被调用。`on_delete` 事件触发器在用户删除数据表中的单元格时被调用。

最后一个要了解的事件触发器是 `on_column_resize`。`on_column_resize` 允许我们响应用户拖动列之间的分隔栏。事件触发器返回正在调整的列 `col` 和我们定义的新宽度 `width`。返回的 `col` 是一个字典，例如：`\{'title': 'Name', 'type': 'str', 'group': 'Data', 'width': 198, 'pos': 1}`。然后，我们在状态中定义的 `self.cols` 中索引并使用此代码更改该列的 `width`：`self.cols[col['pos']]['width'] = width`。



