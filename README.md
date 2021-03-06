
# Student Debt Calculator

[![Build Status](https://travis-ci.org/cfpb/student-debt-calculator.svg?branch=master)](https://travis-ci.org/cfpb/student-debt-calculator)

> A JavaScript package which calculates student debt at graduation based on a wide array of possible inputs.

This calculator does not simply calculate debt based on loans - given inputs of costs, grants, scholarships, personal savings, and loans, it can calculate how much of the annual cost of attendance is left to pay, total debt at graduation, and monthly payment at graduation, based on combined loans and given loan rates.

__Currently in Beta__

## Dependencies
The package runs on [node.js](http://nodejs.org/). It can be included in front-end projects as an npm package - see 'Installation' below.

## Installation
1. Install node.js
2. Run `npm install student-debt-calc --save`

## Usage
`var studentDebtResult = studentDebtCalculator( financials )`

While the command is simple, the key is the `financials` parameter, which is an Object. Here is a sample `financials` Object:

```
var financials = {
    tuitionFees: 10000,
    roomBoard: 2000,
    books: 1000,
    transportation: 500,
    otherExpenses: 250,
    scholarships: 0,
    pell: 0,
    savings: 0,
    family: 0,
    perkins: 0,
    staffSubsidized: 0,
    staffUnsubsidized: 0,
    institutionalLoan: 0,
    privateLoan: 13750,
    undergrad: true
}
```
The script returns an Object (we'll call it `studentDebtResult`, as in the example above), formatted in the same manner as the input, but with calculations made (and new/updated Object properties.

### The financials object

The object passed to `studentDebtCalculator` is used to set up the calculations. Each property has a default value, so properties whose value does not need to be changed from the default can be omitted. Below, we list all the properties used in the calculations. They are separated by category for ease of reading.

#### Costs of Attendance
These values are all added together to get the cost of attendance. They are taken as separate values to match with the [Financial Aid Shopping Sheet](http://www2.ed.gov/policy/highered/guid/aid-offer/index.html).

| Property | Type | Description | Default value |
|-----|-----|-----|-----|
|`financials.tuitionFees` | number | The value of tuition and fees | 0 |
|`financials.roomBoard` | number | The cost of room and board | 0 |
|`financials.books` | number | The cost of books | 0 |
|`financials.otherExpenses` | number | The cost of miscellaneous expenses | 0 |
|`financials.transportation` | number | The costs of transporation | 0 |

#### Grants and Scholarships
These values are deducted from cost of attendance.

| Property | Type | Description | Default value |
|-----|-----|-----|-----|
|`financials.scholarships` | number | Total value of scholarships | 0 |
|`financials.pell` | number | Total value of Pell grants | 0 |

#### Contributions

| Property | Type | Description | Default value |
|-----|-----|-----|-----|
|`financials.workstudy` | number | Value of work-study | 0 |
|`financials.savings` | number | Total personal savings to be spent to reduce annual cost of attendance | 0 |
|`financials.family` | number | Total family contributions to be spent to reduce annual cost of attendance | 0 |

#### Federal Loans

| Property | Type | Description | Default value |
|-----|-----|-----|-----|
|`financials.perkins` | number | Amount of federal Perkins loan | 0 |
|`financials.staffSubsidized` | number | Amount of federal Stafford subsidized loan | 0 |
|`financials.staffUnsubsidized` | number | Amount of federal Stafford unsubsidized loan | 0 |
|`financials.gradPlus` | number | Amount of GradPlus loan | 0 |

#### Private Loans

| Property | Type | Description | Default value |
|-----|-----|-----|-----|
|`financials.institutionalLoanRate` | number | Loan rate on institutional loan, expressed as a decimal | 0.079 |
|`financials.privateLoan` | number | Amount of private loan | 0 |
|`financials.privateLoanMulti`| Array | Used for multiple private loans. This array should contain objects, with each object having two properties - `amount` for the amount of the loan, `rate` for the loan's rate expressed as a decimal, and `deferPeriod` for the number of months the loan is deferred. Example: `[ { 'amount': 3000, 'rate': 0.061, 'deferPeriod': 6 }, { 'amount': 3600, 'rate': 0.059, 'deferPeriod': 6 } ]` __Important note:__ If `privateLoanMulti` is not empty, then the values of `privateLoanMulti` are used and the value of `privateLoan` is ignored! | `[]` (empty array) |
|`financials.homeEquity` | number | Amount of home equity loan | 0 |

#### Loan rates

| Property | Type | Description | Default value |
|-----|-----|-----|-----|
|`financials.institutionalLoanRate` | number | Loan rate for institutional loan, expressed as a decimal | 0.079 |
|`financials.privateLoanRate` | number | Loan rate for private loan, expressed as a decimal | 0.079 |
|`financials.perkinsRate` | number | Loan rate for federal Perkins loans | 0.05
|`financials.subsidizedRate` | number | Loan rate for Stafford subsidized loans | 0.0466
|`financials.unsubsidizedRateUndergrad` | number | Loan rate for Stafford unsubsidized undergratuate loans | 0.0466
|`financials.unsubsidizedRateGrad` | number | Loan rate for Stafford unsubsidized gratuate loans| 0.0621
|`financials.DLOriginationFee` | number | Origination fee for Stafford loans | 1.01073
|`financials.gradPlusRate` | number | Loan rate for GradPLUS loan | 0.0721
|`financials.parentPlusRate` | number | Loan rate for ParentPLUS loan | 0.0721
|`financials.plusOriginationFee` | number | Origination fee for Plus loans | 1.04292
|`financials.homeEquityLoanRate` | number | Loan rate for home equity loan | 0.079

#### Maximums and Caps
These properties give the calculator caps and maximums on certain values.

| Property | Type | Description | Default value |
|-----|-----|-----|-----|
|`financials.perkinsUnderCap` | number | Cap on undergratuate Perkins loans | 5500 |
|`financials.perkinsGradCap` | number | Cap on graduate Perkins loans | 8000 |

## How to test the software

Run tests with:

```
npm test
```

## Getting help
If you have questions, concerns, bug reports, etc, please file an issue in this repository's Issue Tracker.

## License

The project is in the public domain within the United States, and
copyright and related rights in the work worldwide are waived through
the [CC0 1.0 Universal public domain dedication](http://creativecommons.org/publicdomain/zero/1.0/).

All contributions to this project will be released under the CC0
dedication. By submitting a pull request, you are agreeing to comply
with this waiver of copyright interest.

Software source code previously released under an open source license and then modified by CFPB staff is considered a "joint work" (see 17 USC § 101); it is partially copyrighted, partially public domain, and as a whole is protected by the copyrights of the non-government authors and must be released according to the terms of the original open-source license.

For further details, please see: http://www.consumerfinance.gov/developers/sourcecodepolicy/
