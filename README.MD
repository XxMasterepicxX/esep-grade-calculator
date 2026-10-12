# ESEP Grade Calculator

A small Go library that computes a student's final letter grade from three kinds of grades: assignments, exams, and essays.

## How the grade is calculated

1. Each category is averaged on its own.
2. The averages are weighted and summed: assignments 50%, exams 35%, essays 15%.
3. The weighted score becomes a letter: A is 90 and up, B is 80 and up, C is 70 and up, D is 60 and up, anything lower is F.

## Project layout

```
README.MD
grade-calculator/
  go.mod                     module esep/grade-calculator
  grade_calculator.go        the library, package esepunittests
  grade_calculator_test.go   unit tests
```

All Go commands run from inside `grade-calculator/`. That folder name uses a hyphen, not an underscore.

## Setup

1. Install Go 1.24.4 or newer from https://go.dev/dl/. The version comes from `go.mod`.
2. Check the install with `go version`.
3. Clone the repo and move into the module folder:

```
git clone https://github.com/XxMasterepicxX/esep-grade-calculator.git
cd esep-grade-calculator/grade-calculator
```

There are no third party dependencies, so there is nothing else to install.

## Running the tests

```
go test ./...
```

Add `-v` to see each test by name:

```
go test -v ./...
```

## Code coverage

Print the coverage percentage:

```
go test -cover ./...
```

Save a coverage profile, then view it per function or as an HTML page with covered lines in green and missed lines in red:

```
go test -coverprofile=coverage.out ./...
go tool cover -func=coverage.out
go tool cover -html=coverage.out
```

`coverage.out` is a generated file. Don't commit it.

## Using the library

```go
gc := NewGradeCalculator()
gc.AddGrade("open source assignment", 95, Assignment)
gc.AddGrade("exam 1", 88, Exam)
gc.AddGrade("essay on ai ethics", 91, Essay)

letter := gc.GetFinalGrade() // "A", "B", "C", "D", or "F"
```

Grades are whole numbers. Add at least one grade of each type before calling `GetFinalGrade`. An empty category makes the average divide by zero and the program panics.
