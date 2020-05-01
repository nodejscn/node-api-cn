<!-- YAML
changes:
  - version:
      - v13.9.0
      - v12.16.2
    pr-url: https://github.com/nodejs/node/pull/31386
    description: Workers are now included in the report.
-->

[`Worker`][] threads can create reports in the same way that the main thread
does.

Reports will include information on any Workers that are children of the current
thread as part of the `workers` section, with each Worker generating a report
in the standard report format.

The thread which is generating the report will wait for the reports from Worker
threads to finish. However, the latency for this will usually be low, as both
running JavaScript and the event loop are interrupted to generate the report.



