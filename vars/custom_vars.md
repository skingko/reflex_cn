```python exec
import reflex as rx

from pcweb.pages.docs import vars
```
# 自定义变量

正如在[变量页面]({vars.base_vars.path})中所提到的，Reflex变量必须是可以被JSON序列化的。

这意味着我们可以支持任何Python的原始类型，以及列表、字典和元组。但是，您也可以通过继承 `rx.Base` 来创建更复杂的变量类型。

## 定义一个类型

在这个例子中，我们将创建一个自定义的变量类型用于存储翻译。

一旦定义好了，我们就可以将它用作状态变量，并在组件内部引用它。

```python demo exec
import googletrans

class Translation(rx.Base):
    original_text: str
    translated_text: str

class TranslationState(rx.State):
    input_text: str = "Hola Mundo"
    current_translation: Translation = Translation(original_text="", translated_text="")

    def translate(self):
        text = googletrans.Translator().translate(self.input_text, dest="en").text
        self.current_translation = Translation(original_text=self.input_text, translated_text=text)


def translation_example():
    return rx.vstack(
        rx.input(on_blur=TranslationState.set_input_text, default_value=TranslationState.input_text, placeholder="Text to translate..."),
        rx.button("Translate", on_click=TranslationState.translate),
        rx.text(TranslationState.current_translation.translated_text),
    )
```

