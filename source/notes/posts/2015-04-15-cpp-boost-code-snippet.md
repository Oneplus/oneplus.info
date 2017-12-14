---
layout: note
title: Useful code snippets with C++ boost
author: Oneplus
category: ["Programming"]
tags:
    - "C/C++"
    - "boost"
---

# Is Punctuation

It's very straight forward to use `boost.regex` as a solution. We can match the input string with a regex like

```
if (boost::regex_match(",", boost::regex("[[:punct:]]"))) {
      std::cout << "is punctuation." << std::endl;
}
```

If the ICU is also in our consideration, code should be modified as

```
if (boost::u32regex_match("！", boost::make_u32regex("[[:P*:]]"))) {
      std::cout << "is unicode punctuation." << std::endl;
}
```

# Argument Parser

Like `optparse.OptionParser` in Python, boost also provides a very nice command line arguments parser, in `<boost/program_options.hpp>`.

### 2017-12-14 updates

Now, it's `argparse.ArgumentParser`.
