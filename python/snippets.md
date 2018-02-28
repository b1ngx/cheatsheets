# snippets

清除 html 中的属性和空格

```
import lxml.html.clean as clean
import re

whitespace_re = re.compile("\s+")


clean_html = whitespace_re.sub('', clean.Cleaner(
            safe_attrs_only=True,
            safe_attrs=frozenset()
        ).clean_html(content))
```

