# Strive for Fluent Usage (자연스러운 사용을 위해 노력하기)

- >**Prefer method and function names that make user sites form grammartical English phrases.**

- >**Begin names of factory methods with** "make", e.g. x.makeIterator().

- >The first argument to **initializer and** factory methods calls should not form a phrase starting with the base name, e.g. x.makeWidget(cogCount: 47)

- >**Name functions and methods according to their side-effects**

- >**Uses of Boolean methods and properties should read as assertions about the receiver** when the use is nonmutating, e.g. x.isEmpty, line1. intersects(line2).

- >**Protocols that describe what something is should read as nouns** (e.g. Collection).

- >**Protocols that describe a capability should be named using the suffixes** able, ible, **or** ing (e.g. Equatable, ProgressReporting).

- >The names of other **types, properties, variables, and constrants should read as nouns.**

