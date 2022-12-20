# Use Terminology Well (적절한 부분에 기술용어 잘 사용하기)

### Term of Art (기술 용어)   

- > noun - a word or phrase that has a precise,   
  specialized meaning within a particular field or profession.

  명사 - 특정 분야나 직군 내에서 정확하고 전문적인 의미를 가진 단어 혹은 구.

- >**Avoid obscure terms** if a more common word conveys meaning just as well.   
    Don't say "epidermis" if "skin" will serve your purpose.   
    Terms of art are an essential communication tool,   
    but should only be used to capture crucial meaning that would otherwiser be lost.

    만약 일반적으로 사용되는 단어로도 충분히 의미가 전달된다면 **`이해하기 힘든 모호한 용어는 사용하지 않도록 합니다.`**   
    `"피부"`라는 단어만으로도 의도가 전달된다면, `"표피"`라는 단어는 사용하지 않습니다.   
    기술 용어는 중요한 소통 수단이지만, 이를 사용하지 않고서는 용어가 가진 중요한 의미를 담을 수 없을 경우에만 사용해야 합니다.

- >**Stick to the established meaning** if you do use a term of art.

    만약 기술 용어를 사용한다면 **용어가 가지고 있는 의미에 충실하도록 사용해야 합니다.**
    
    ## 🔎 MORE DETAIL
    - > The only reason to use a technical term rather than a more common word is that it precisely expresses something that would otherwise be ambiguous or unclear.   
    Therefore, an API should use the term strictly in accordance with its accepted meaning.   

        다른 용어를 사용함으로써 그 의미가 모호해지고 불명확해질 경우   
        이를 명확하게 하고자할 때만 기술 용어를 사용해야합니다.   
        따라서, API에서 사용되는 용어는 그 의미가 어떻게 받아들여질지를 고려해서 엄격하게 선별하여 사용해야합니다.

    - > **`Don't surprise an expert:`** anyone already familiar with the term will be surprised and probably angered if we appear to have invented a new meaning for it.

        **`전문가를 놀라지 않도록 합니다.`**:   
        만약 용어를 기존의 의미가 아닌 쓰이지 않던 새로운 의미로써 사용한다면   
        그 용어에 대해 이미 익숙한 사람은 경악하고 불쾌해 할 것입니다.   

    - > **`Don't confuse a beginner:`** anyone trying to learn the term is likely to do a web search and find its traditional meaning.

        **`초심자 입장에서 혼동되지 않도록 합니다.`**:   
        누군가는 웹 검색을 통해 사용된 용어가 가지고 있는 고유한 의미를 찾아내려고 할 것입니다.

- >**Avoid abbreviations.**   
    Abbreviations, especially non-standard ones, are effectively terms-of-art, because understanding depends on correctly translating them into their non-abbreviated forms.

    **`축약어를 피하도록 합니다.`**   
    특히 표준 축약어가 아닌 축약어들은 실질적으로 기술 용어입니다.   
    축약되지 않은 표현으로 얼마나 잘 번역하는지에 따라 그 기술 용어에 대한 이해도가 달라기지 때문입니다.   
    (따라서 누구나 쉽게 이해할 수 있도록 축약어를 피하는 것이 좋습니다.)
        
    - > The intended meaning for any abbreviation you use should be easily found by a web search.

        축약어를 사용할 때 의도했던 의미를 웹 검색으로 쉽게 찾을 수 있어야 합니다.

- >**Embrace precedent.**   
    Don't optimize terms for the total beginner at the expense of conformance to existing culture.

    **`선계를 따르도록 합니다.`**   
    일반적으로 사용해오던 기존의 용어를 대체하면서까지 초심자의 눈높이에 맞춰 용어를 최적화하지 않도록 합니다.   

    ## 🔎 MORE DETAIL
    - > It is better to name a contiguous data structure `Array` than to use a simplified term such as `List`,   
    even though a beginner might grasp the meaning of List more easily.   
    Arrays are fundamental in modern computing,   
    so every programmer knows-or will soon learn-what an array is.   
    Use a term that most programmers are familiar with,   
    and their web searches and questions will be rewarded.

        연속적으로 자료구조의 이름으로 `List`보다 `Array`를 사용하는 것이 좋습니다.   
        `List`를 사용하는 것이 초심자에게는 그 뜻을 이해하기에 더 쉬울지 모르지만 말입니다.   
        `Array`는 현대 컴퓨팅의 기초이기 때문에 모든 프로그래머들이 알고 있고,   
        설령 아직 배우지 않은 프로그래머일지라도 곧 배우게 됩니다.   
        대부분의 프로그래머들에게 익숙한 용어를 사용하면 웹 검색과 질문을 통해 그 의미를 쉽게 찾을 수 있습니다.   

    - > Within a particular programming domain, such as mathematics,   
    a widely precedented term such as `sin(x)` is preferable to an explanatory phrase such as `verticalPositionOnUnitCircleAtOriginOfEndRadiusWithAngle(x)`.    
    Note that in this case, precedent outweighs the guideline to avoid abbreviations: although the complete word is sine,   
    `"sin(x)"`has been in common use among programmers for decades,   
    and among mathematicians for centuries.

    수학과 같은 특정 프로그래밍 도메인에서 `sin(x)`와 같은 용어는 해당 표현의 의미를 풀어서 설명한   
    `verticalPositionOnUnitCircleAtOriginOfEndRadiusWithAngle(x)` 보다   
    일반적으로 사용되고 있는 `sin(x)`를 사용하는 것이 좋습니다.   
    `sin(x)`는 축약어 이지만 이 경우 축약어를 피하라는 권장 지침을 지키는 것 이상으로   
    기존에 사용해왔던 선례를 따르는 것이 중요하다는 점에 유의하도록 합니다:   
    비록 정확한 단어는 `sine`이지만, 수 십 년간 프로그래머들과 또 수 세기 동안 수학자들 사이에서는 `"sin(x)"`라는 표현이 일반적으로 사용되어 왔습니다.   