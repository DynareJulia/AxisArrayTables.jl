# AxisArrayTables

Tables backed by AxiArrays

## Constructors

```
AxisArrayTable(data::AbstractMatrix, rows::AbstractVector, cols::Vector{Symbol}
AxisArrayTable(table)
```

## Accessors

```
data(m::AxisArrayTable)
named_axes(m::AbstractAxisArrayTable)
row_labels(m::AbstractAxisArrayTable)
column_labels(m::AbstractAxisArrayTable)
```
## Lag, lead and diff
lag(m::AbstractAxisArrayTable, args...)
lead(m::AbstractAxisArrayTable, args...)

## Example
```
julia> using AxisArrayTables
julia> using ExtendDates
julia> aat = AxisArrayTable(rand(3,2), QuarterSE(2000,2):QuarterSE(2000,4), [:x, :y])
┌──────────┬───────────┬───────────┐
│         │        x │        y │
├──────────┼───────────┼───────────┤
│ 2000-Q2 │ 0.826987 │ 0.733659 │
│ 2000-Q3 │ 0.857407 │  0.16946 │
│ 2000-Q4 │ 0.324339 │ 0.384603 │
└──────────┴───────────┴───────────┘
julia> row_labels(aat)
QuarterSE("2000-Q2"):Quarter(1):QuarterSE("2000-Q4")
julia> column_labels(aat)
2-element Vector{Symbol}:
 :x
 :y
julia> lag(aat)
┌──────────┬───────────┬───────────┐
│         │        x │        y │
├──────────┼───────────┼───────────┤
│ 2000-Q2 │  missing │  missing │
│ 2000-Q3 │ 0.826987 │ 0.733659 │
│ 2000-Q4 │ 0.857407 │  0.16946 │
└──────────┴───────────┴───────────┘


julia> lead(aat)
┌──────────┬───────────┬───────────┐
│         │        x │        y │
├──────────┼───────────┼───────────┤
│ 2000-Q2 │ 0.857407 │  0.16946 │
│ 2000-Q3 │ 0.324339 │ 0.384603 │
│ 2000-Q4 │  missing │  missing │
└──────────┴───────────┴───────────┘ 
```

