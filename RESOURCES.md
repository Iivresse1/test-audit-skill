# Test-Audit Skill Resources

## Knowledge

- [Paper: The Oracle Problem in Software Testing: A Survey](https://discovery.ucl.ac.uk/id/eprint/1471263/1/06963470.pdf)
  Defines the test-oracle problem and surveys specifications, models, contracts, metamorphic testing, and human judgment. Use for: deciding where independent expected behavior can come from.
- [Stryker: Mutant states and metrics](https://stryker-mutator.io/docs/mutation-testing-elements/mutant-states-and-metrics/)
  Official definitions of killed, survived, uncovered, and invalid mutants. Use for: interpreting dynamic evidence without overclaiming.
- [PIT: Basic concepts](https://pitest.org/quickstart/basic_concepts/)
  Official mutation-testing concepts, including survived and equivalent mutations. Use for: Java-oriented examples and mutation caveats.
- [Microsoft Learn: Mutation testing for .NET](https://learn.microsoft.com/en-us/dotnet/core/testing/mutation-testing)
  Practical mutation example and explicit warning against chasing a perfect mutation score. Use for: explaining mutation as evidence rather than a universal quality score.
- [Google Testing Blog: Test Behavior, Not Implementation](https://testing.googleblog.com/2013/08/testing-on-toilet-test-behavior-not.html)
  Explains the maintenance and validity risks of coupling tests to implementation details. Use for: separating behavior contracts from private mechanics.
- [Paper: An Empirical Evaluation of Manually Created Equivalent Mutants](https://arxiv.org/abs/2404.09241)
  Studies mutants that change syntax without changing semantics. Use for: understanding why a surviving mutation is not automatically a test defect.

## Wisdom (Communities)

No community selected yet. Prefer maintainers and practitioner communities for the mutation tool used by the target project.

## Gaps

- Real open-source before-and-after examples still need to be curated against the final taxonomy.
- The first skill's supported test levels and ecosystems are not settled yet.

