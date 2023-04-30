# renovate-repro-gitlab-ref-multi-line

Minimal reproduction of Renovate's crash when parsing a multi-line !reference tag in a GitLab CI/CD template.

## Steps to reproduce

1. Enable the Renovate manager `gitlabci`
1. In a GitLab CI/CD template, add [a `!reference` tag](https://docs.gitlab.com/ee/ci/yaml/yaml_optimization.html#reference-tags) that spreads over multiple lines, like:

    ```yaml
    .base:
      script:
        - mytool

    myjob:
      script:
        - !reference [
          .base,
          script,
        ]
    ```

1. Renovate will crash with `YAMLException: unknown tag !<!reference>` when parsing the file
