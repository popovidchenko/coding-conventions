@param - Описывает параметр метода или функции. Например, @param parameterName Описание параметра.
@return - Описывает возвращаемое значение метода или функции. Например, @return Описание возвращаемого значения.
@brief - Краткое описание следующего за ним объявления. Например, @brief Краткое описание класса или метода.
@details - Более подробное описание, следующее за кратким описанием, если таковое имеется.
@warning - Предупреждение о возможных проблемах при использовании метода или функции.
@note - Примечание, содержащее важную информацию о методе или функции.
@see - Ссылка на связанные функции, методы или другие элементы документации.
@since - Указывает, с какой версии программы или библиотеки введен элемент.
@deprecated - Указывает, что элемент устарел и может быть удален в будущих версиях.

***

1. Для улучшение навигации и организации кода рекомендуется использовать аннотации Xcode. Они имеют встроенную поддержку и облегчают работу с кодом.
`// TODO: ` используется для отметки того, что необходимо выполнить определённые задачи или добавить функциональность в будущем.
`// FIXME: ` применяется для указания на части кода, которые содержат ошибки или требуют исправления.
`// MARK: ` позволяет добавлять метки для разделения кода на логические секции.
`// !!!: ` используется для отметки места, на который следует обратить внимание.
`// ???: ` применяется для обозначения вопроса или необходимости обсуждения.

2. Переменные экземпляра имеют префикс _.

3. Константы имеют префикс k.

4. When using properties, instance variables should always be accessed and mutated using self.. This means that all properties will be visually distinct, as they will all be prefaced with self..
An exception to this: inside initializers, the backing instance variable (i.e. _variableName) should be used directly to avoid any potential side effects of the getters/setters.

5. Property attributes should be explicitly listed, and will help new programmers when reading the code. The order of properties should be storage then atomicity, which is consistent with automatically generated code when connecting UI elements from Interface Builder.

Properties with mutable counterparts (e.g. NSString) should prefer copy instead of strong. Why? Even if you declared a property as NSString somebody might pass in an instance of an NSMutableString and then change it without you noticing that.

6. Dot syntax is purely a convenient wrapper around accessor method calls. When you use dot syntax, the property is still accessed or changed using getter and setter methods. Read more here

Dot-notation should always be used for accessing and mutating properties, as it makes code more concise. Bracket notation is preferred in all other instances.

7.Constants
Constants are preferred over in-line string literals or numbers, as they allow for easy reproduction of commonly used variables and can be quickly changed without the need for find and replace. Constants should be declared as static constants and not #defines unless explicitly being used as a macro.

8. Комментарии

When they are needed, comments should be used to explain why a particular piece of code does something. Any comments that are used must be kept up-to-date or deleted.

Declaration Comments /** ... */
Every non-trivial interface, public and private, should have an accompanying comment describing its purpose and how it fits into the larger picture.

Comments should be used to document classes, properties, ivars, functions, categories, protocol declarations, and enums.

Implementation Comments //
Provide comments explaining tricky, subtle, or complicated sections of code.

9. Имена аутлетов содержат название сущностей, которыми они являются (View, Image, Button и т.п.);
