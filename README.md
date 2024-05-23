# component-readiness-triage

Counterpart to [sippy gen-resolved-issue.py](https://github.com/openshift/sippy/tree/master/hack) containing triage template and regression data for evaluation / persistence.

`export GEN_RESOLVED_ISSUE=/path/to/gen-resolved-issue.py`

`export GOOGLE_APPLICATION_CREDENTIALS=/path/to/credentials.json`

In general when regressions are triaged they are done individually as needed.

`$GEN_RESOLVED_ISSUE --input-file my_template.json`

`$GEN_RESOLVED_ISSUE --output-type=DB --load-incidents-from-file=True --input-file my_regressions.json`

This can potentially be automated / scripted utilizing the `--relative-sample-time` flag

Update all regression files
```
for f in *template.json; do $GEN_RESOLVED_ISSUE --relative-sample-times=True --input-file $f; done
```

Persist all regressions

```
for f in *regressions.json; do $GEN_RESOLVED_ISSUE --output-type=DB --load-incidents-from-file=True --input-file $f; done
```

For the really brave, skip the intermediate regressions output file (may require removing `OutputFile` from the template)

```
for f in *template.json; do $GEN_RESOLVED_ISSUE --output-type=DB --relative-sample-times=True --input-file $f; done
```
