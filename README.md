# CEL Task for Tekton

This repo provides an experimental [Tekton Custom
Task](https://github.com/tektoncd/community/pull/128) that, when run, simply
evaluates a [CEL](https://github.com/google/cel-spec) expression passed as a
parameter, and fails if the result is `false`, or a non-boolean value, or if
the expression is invalid or can't be evaluated.

The intention is to demonstrate the kinds of things a Custom Task can do, and
to demonstrate how to write a Custom Task.

## Install

Install and configure `ko`.

```
ko apply -f controller.yaml
```

This will build and install the controller on your cluster, in the namespace
`cel-task`.

## Run a CEL Task

```
$ kubectl create -f cel-run.yaml 
run.tekton.dev/cel-run-fqqjt created
$ kubectl get runs
NAME            SUCCEEDED   REASON           STARTTIME   COMPLETIONTIME
cel-run-fqqjt   True        ExpressionTrue   2s          2s
```

If you change the expression in `cel-run.yaml` to something that evaluates to
`false`, or an invalid CEL expression, the Task will fail instead.
