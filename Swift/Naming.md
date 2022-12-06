# Naming

## Promote Clear Usage (명확하게 사용하기)
- >**Include all the words needed to avoid ambiguity** for a person reading code where the name is used.   

    이름이 사용된 코드를 읽는 사람들을 위해 **모호함으로 혼동을 주지 않도록 필요한 모든 단어를 포함합니다.**

- >**Omit needless words.**
    Every word in a name should convery salient information at the use site.   

    **불필요한 단어는 생략합니다.**   
    이름의 모든 단어는 사용 장소에서 중요한 정보를 전달해야합니다.

- >**Name variables, parameters, and associated types according to their roles,** rather than their type constraints.   

    타입 제약이 아닌 **해당 역할에 따라 변수, 매개변수, 그리고 연관된 타입의 이름을 붙입니다.**

- >**Compensate for weak type information** to clarify a parameter's role.   

    매개변수의 역할을 명확하게 하기 위하여 **약한 정보 타입을 보완합니다.**

---
## Strive for Fluent Usage (자연스러운 사용을 위해 노력하기)
- >**Prefer method and function names that make user sites form grammartical English phrases.**

- >**Begin names of factory methods with** "make", e.g. x.makeIterator().

- >The first argument to **initializer and** factory methods calls should not form a phrase starting with the base name, e.g. x.makeWidget(cogCount: 47)

- >**Name functions and methods according to their side-effects**

- >**Uses of Boolean methods and properties should read as assertions about the receiver** when the use is nonmutating, e.g. x.isEmpty, line1. intersects(line2).

- >**Protocols that describe what something is should read as nouns** (e.g. Collection).

- >**Protocols that describe a capability should be named using the suffixes** able, ible, **or** ing (e.g. Equatable, ProgressReporting).

- >The names of other **types, properties, variables, and constrants should read as nouns.**

---
## Use Terminology Well (적절한 부분에 기술용어 잘 사용하기)
>**Term of Art**   
noun - a word or phrase that has a precise, specialized meaning within a particular field or profession.

- >**Avoid obscure terms** if a more common word conveys meaning just as well.   
    Don't say "epidermis" if "skin" will serve your purpose.   
    Terms of art are an essential communication tool,   
    but should only be used to capture crucial meaning that would otherwiser be lost.

- >**Stick to the established meaning** if you do use a term of art.   

- >**Avoid abbreviations.**   
    Abbreviations, especially non-standard ones, are effectively terms-of-art, because understanding depends on correctly translating them into their non-abbreviated forms.
        
    > The intended meaning for any abbreviation you use should be easily found by a web search.

- >**Embrace precedent.**   
    Don't optimize terms for the total beginner at the expense of conformance to existing culture.