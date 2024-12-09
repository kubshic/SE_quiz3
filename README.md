[![Review Assignment Due Date](https://classroom.github.com/assets/deadline-readme-button-22041afd0340ce965d47ae6ef1cefeee28c7c493a6346c4f15d667ab976d596c.svg)](https://classroom.github.com/a/z8VxFEdO)
# Quiz #3: Statement locator

This quiz is inspired by this following research work:

*[1] C. Le Goues, M. Dewey-Vogt, S. Forrest, and W. Weimer, “A systematic study of automated program repair: Fixing 55 out of 105 bugs for $8 each,” in 2012 34th International Conference on Software Engineering (ICSE), Jun. 2012, pp. 3–13. doi: 10.1109/ICSE.2012.6227211.*


Your submission must satisfy the following requirements:

* R1. Shall initialize your assignment repository by GitHub Classroom.
* R2. Write your `StatRepair.py` in the repository.
* R3. Test your `StatRepair.py` by using `pytest`.
* R4. You need to let your TA know your repository URL and your student ID together.
* R5. `StatRepair` class should be defined in the `StatRepair.py`
* R6. The above class is tested as:

```
from StatRepair import StatRepair
from urlparse import urlparse

def test_urlparse():
    debugger = StatRepair()

    with debugger.collect_pass():
        urlparse("http://aaaa.com")

    with debugger.collect_pass():
        urlparse("http://aaaa.com#aaa#bbb")

    with debugger.collect_pass():
        urlparse("https://[2001:db8:85a3:8d3:1319:8a2e:370:7348]:443/")

    with debugger.collect_fail():
        urlparse("http://aaaa.com#aaa#bbb;;;")

    line, dist = debugger.mostsimilarstmt(target)

    assert ...
```

* R7. This assignment assumes that you already have a `RankingDebugger`, `ContinuousSpectrumDebugger`, and `OchiaiDebugger` class composed from `debuggingbook.org`, and uses the Ochiai metric (https://www.debuggingbook.org/html/StatisticalDebugger.html#The-Ochiai-Metric).
* R8. You have to add `line, dist = mostsimilarstmt(targetloc)` to your debugger class, where:
   - `targetloc` -- A pair of (`function name`, `linu number`). A suspicious location in the target program. Usually, this is designated by `debugger.rank()[x]`
   - `line` -- A string representing the most similar line with the statement at the `targetloc`. This should be a stripped string.
   - `dist` -- An integer value representing the Levenshtein distance between the statement at the `targetloc` and `line`.
* R9. The return value of `mostsimilarstmt(targetloc)` shall avoid statements with `dist == 0` as the statements identical with the buggy statement are useless.
* R10. The Levenshtein distance shall be computed after stripping the statements.
* R11. Installing new packages is not allowed. Shall assume that all packages are installed for `debuggingbook`.




## Note:

* N1. `pytest` (based on `test_urlparse*.py`) is just for validating your program. The final grading will be made by other test cases.
* N2. Submissions via GitHub Classroom will only be accepted. Submissions via LMS or any other means are not accepted.
* N3. DO NOT change files in this repository except for `StatRepair.py`. Adding new files are allowed.
* N4. DO NOT use any other packages other than specified ones in `requirements.txt`.
