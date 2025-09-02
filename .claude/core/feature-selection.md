# Feature Selection

## Logic
With arg: Find matching directory in features/*, confirm if not found
No arg: List all features, ask for selection
Never auto-select even with single feature - always confirm

## Error Messages
Not found: "Feature '[name]' not found. Available: [list]. Please specify existing feature."
No features: "No features found. Run `/pin:plan` or `/pin:feature` first."

## Display Format
"Available features:
1. 01-feature-name
2. 02-another-feature
Select feature number or name:"