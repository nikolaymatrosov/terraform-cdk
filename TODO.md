### Related issue

Fixes #3915

### Description

This PR adds support for `StringMapMap` type to handle provider schemas that define attributes with `map[map[string]]` type structure. The yandex-cloud provider (and potentially others) define certain attributes like `airflow_config` with a nested map structure that wasn't previously supported by the CDKTF code generation.

The implementation includes:

1. **New `StringMapMap` class**: Added to `packages/cdktf/lib/complex-computed-list.ts` that extends `ComplexResolvable` and provides a `lookup(key: string): StringMap` method for accessing nested maps
2. **Provider generator updates**: Modified `attribute-type-model.ts` to detect when the element type is `StringMap` and generate the appropriate `StringMapMap` type instead of the generic pattern
3. **Comprehensive tests**: Added test fixtures and snapshots to ensure the new functionality works correctly

The fix enables users to successfully generate providers that use nested map structures in their schemas, resolving the JSII compilation errors that were preventing provider generation.

### Checklist

- [x] I have updated the PR title to match [CDKTF's style guide](https://github.com/hashicorp/terraform-cdk/blob/main/CONTRIBUTING.md#pull-requests-1)
- [x] I have run the linter on my code locally
- [x] I have performed a self-review of my code
- [x] I have commented my code, particularly in hard-to-understand areas
- [x] I have made corresponding changes to the documentation if applicable
- [x] My changes generate no new warnings
- [x] I have added tests that prove my fix is effective or that my feature works if applicable
- [x] New and existing unit tests pass locally with my changes