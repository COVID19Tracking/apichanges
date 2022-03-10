---

title: The COVID Tracking Project API Changelog

---

# COVID Tracking Project API Changelog

## About

The COVID Tracking Project (CTP) hosted a data API with numbers for COVID-19 testing, outcomes, and hospitalization. This file includes publicly announced changes to the data API. The changelog was hosted and donated by [Headway](https://headwayapp.co/), and exported to this single markdown-formatted file by CTP staff.

Related links:

- [Original data API page](https://covidtracking.com/data/api/)
- [Original change log](https://apichanges.covidtracking.com/)

## Changelog entries

### Ending support for CORS requests May 1, 2021

**Posted April 28, 2021**

As [announced in February](https://apichanges.covidtracking.com/it-s-time-the-covid-tracking-project-will-soon-come-to-an-end-184739), the COVID Tracking Project's API will be winding down in May. The first step in this process will be disabling support for CORS and removing redirects for our old services.

CORS Support enabled many developers to quickly build apps on our infrastructure without servers. However, a handful of poorly-built applications take up the bulk of our traffic, and they are all using CORS. We suggest caching our data within your own application.

### New field: hospitalizedDischarged

**Posted February 22, 2021**

We have added a new field, `hospitalizedDischarged` for several states. More states will be added as we get data:

- AZ
- CO
- CT
- IN
- KS
- NC
- NJ
- NY
- RI
- VA

### It’s Time: The COVID Tracking Project Will Soon Come to an End

**Posted February 3, 2021**

After a year of collecting, analyzing, and interpreting COVID-19 data for the United States, we’re [ending our data compilation work in early March](https://covidtracking.com/analysis-updates/covid-tracking-project-end-march-7). The [existing API will continue to work until May 2021](https://covidtracking.com/about-data/faq#what-will-happen-to-your-apidata-after-march-7), but will only include data up to March 7, 2021.

### Deprecating state grades

**Posted January 28, 2021**

As part of a move to a new assessment process, we are officially deprecating the field `dataQualityGrade` from our state endpoints. The new state assessment data will be available by February 5 from our [data downloads page](https://covidtracking.com/data/download).

On February 15, we will `null` out the `dataQualityGrade` field.

### Announcing Version 2 of our API

**Posted January 25, 2021**

As the COVID Tracking Project approaches our first year, we have been learning-while-doing with building our API. Our API powers thousand of applications, with millions of users per month, and is core to our mission to provide the most accurate and timely data about COVID in the US to a wide audience.

Our current API is a flat, CSV-file like endpoint, with very little flexibility to add new fields or remove old deprecated ones. Because it was so quickly adopted, we were unable to change these fields around without breaking applications.

Today, we are [announcing a beta of version 2](http://covidtracking.com/data/api/version-2) of our API with the following features:

- Every datapoint includes calculations like percents of population and seven-day averages where appropriate. This can be turned off by requesting a “simple” endpoint
- Endpoints return data in a structured format of categories. For example, instead of `hospitalizedCumulative`, use `outcomes.hospitalized.total`
- Human-readable field titles are included with every endpoint. For example, the states daily endpoint includes definition for `outcomes.hospitalized.total`: Cumulative hospitalized/Ever hospitalized
- All annotations or warnings are included in the state’s metadata

These features were built against an RFP that got considerable public and private feedback from select API users.

#### Will the “v1” API change or go down?

No. We will never take offline or remove features from the v1 API. We may still change deprecated fields as we always have.

#### When will the v2 API be available?

[It is available now](http://covidtracking.com/data/api/version-2), but all URLs are prefixed with `/v2beta`. We will take it out of beta on February 15.

#### How can I provide feedback?

[Feel free to contact us with any questions or concerns](https://covidtracking.com/contact/other) (select "API in the dropdown) about the new API.

### Removing negative test results from various states

**Posted January 12, 2021**

We are [removing negatives that were created from mixed units](https://covidtracking.com/about-data/faq#why-are-you-removing-values-from-the-api-field-negative-from-various-states-starting-on-january-27-2021) (specimens minus cases or test encounters minus cases) for states that are using explicit totals in `totalTestResults`.

As of January 27, 2021, these states will have a `null` value for `negative`.

### National recovered field is now deprecated

**Posted January 8, 2021**

Per [our announcement on November 18, 2020](https://headwayapp.co/the-covid-tracking-project-api-changes/deprecation-of-national-recovered-data-176175) the national `recovered` field in the US endpoints is now deprecated and all US recovered values are now `null`.

### Deprecation of state URLs

**Posted December 14, 2020**

On December 28, we will be deprecating the following fields in the **States metadata** endpoints:

- `covid19Site`
- `covid19SiteOld`
- `covid19SiteSecondary`
- `covid19SiteTertiary`
- `covid19SiteQuaternary`
- `covid19SiteQuinary`

### Deprecation of national recovered data

**Posted November 18, 2020**

On December 2, 2020 we will officially **deprecate** the `recovered` field in our **national** endpoints (i.e. `https://api.covidtracking.com/v1/us/daily.json`).

As of January 8, 2021, this field returns `null`.

[Learn more about why we are deprecating national recovered data](https://covidtracking.com/about-data/faq#why-have-you-stopped-reporting-national-recoveries).

### Zeroing out of deprecated fields

**Posted November 4, 2020**

The following fields in our API have been deprecated for several months, and will start returning `0` or `null` on **November 16**

#### States daily

- `total` - Will return zero, use `totalTestResults` instead
- `posNeg` - Will return zero, use `totalTestResults` instead
- `checkTimeEt` - Will return `null`, use `lastUpdateEt` instead
- `dateModified` - Will return `null`, use `lastUpdateEt` instead
- `dateChecked` - Will return `null`, use `lastUpdateEt` instead
- `hospitalizedIncrease` - Will return `0`, use `currentlyHospitalized` instead
- `hash` - Will return null.

#### US

- `hash` - Will return null
- `hospitalizedIncrease` - Will return `0`, use `currentlyHospitalized` instead
- `lastModified` - Will return `null`, use `lastUpdateEt` instead
- `dateChecked` - Will return `null`, use `lastUpdateEt` instead

### Deprecation of the public spreadsheet

**Posted October 15, 2020**

Since the COVID Tracking Project started in March, we have been collating and publishing our data in the form of a single Google Sheet. Our API and website both used that sheet to publish all our core dataset. As our data collection effort has matured, we have built new tools to improve our publishing process. To that end, all of our API and website data are now based on an improved publishing system that no longer uses Google sheets.

However, people have been using our public sheets to import our data in ways that were never intended. We only support pulling data through our API. Supporting users whose apps broke because we changed the public sheet has had a significant impact on our support teams.

We encourage anyone who is using the public sheet for importing data to switch to our API, or import the CSV files available from our download page. As of **November 30**, the sheet will be static and no longer get new rows or columns, and on **December 24**, it will be taken offline.

### States: Deprecation of totalTestResultsSource

**Posted September 29, 2020**

The field `totalTestResultsSource` in the `states/daily` endpoints are now marked as deprecated, and will return `null` in two weeks.

Instead you should use the field `totalTestResultsField` in the `states/info` endpoint to find out what field is used to compute for `totalTestResults`.

### States info & states daily: New total test results

**Posted September 18, 2020**

The states info endpoint now have a new `totalTestResultsField` field that indicates which field we are pulling from for the state's `totalTestResults` value.

### US daily: Total test results update

**Posted September 17, 2020**

Per our [announcement on US total test results](https://covidtracking.com/about-data/faq#why-did-your-national-total-test-results-numbers-change-on-september-17), the sources of `totalTestResults` are now updated to match our new standards.

While the field `posNeg` has been marked as deprecated since April, we are now returning `0` for that field.

### New fields in States Info

**Posted September 2, 2020**

We are adding two new fields to the states info endpoints (`/v1/states/info.json`, and `v1/states/info.csv`):

- `covidTrackingProjectPreferredTotalTestField` - Locator field that explains which API fields The COVID Tracking Project prefers for each state’s “New tests” chart and on the state’s history page on our website. Selects from the following options in order of priority: totalTestEncountersViral, totalTestsViral, totalTestsPeopleViral, or—where those units are all missing a sufficient time series—totalTestResults.
- `covidTrackingProjectPreferredTotalTestUnits` - Label indicating which units The COVID Tracking Project prefers for each state’s “New tests” chart and on the state’s history page on our website. Selects from the following options in order of priority: test encounters, specimens, people, or—where those units are all missing a sufficient time series—negatives plus positives.

### API field description update

**Posted August 25, 2020**

We have updated our API page to align all field definitions with those in our [data definitions page](https://covidtracking.com/about-data/data-definitions).

### New Testing fields

**Posted August 11, 2020**

On August 14 2020, we will be publishing twelve new API fields in the **states** endpoints for antigen, PCR, and antibody testing:

- Total Test Encounters (PCR) `totalTestEncountersViral`
- Total PCR Tests (People) `totalTestsPeopleViral `
- Total Antibody Tests `totalTestsAntibody`
- Positive Antibody Tests `positiveTestsAntibody`
- Negative Antibody Tests `negativeTestsAntibody`
- Total Antibody Tests (People) `totalTestsPeopleAntibody`
- Positive Antibody Tests (People) `positiveTestsPeopleAntibody`
- Negative Antibody Tests (People) `negativeTestsPeopleAntibody`
- Total Antigen Tests (People) `totalTestsPeopleAntigen`
- Positive Antigen Tests (People) `positiveTestsPeopleAntigen`
- Total Antigen Tests `totalTestsAntigen`
- Positive Antigen Tests `positiveTestsAntigen`

### Deprecation of old URLs

**Posted August 6, 2020**

We are officially deprecating the old API URLs that have been redirecting since April 2 to our current API paths. Users of these old URLs should update their apps before **October 15**, when these paths will start returning 404 errors.

| Old URL                               | New URL                        |
| ------------------------------------- | ------------------------------ |
| /states/info.csv                      | /v1/states/info.csv            |
| /states/daily.csv                     | /v1/states/daily.csv           |
| /states.csv                           | /v1/states/current.csv         |
| /us.csv                               | /v1/us/current.csv             |
| /us/daily.csv                         | /v1/us/daily.csv               |
| /states/daily?state=:state&date=:date | /v1/states/:state/:date.json   |
| /statesdaily?state=:state&date=:date  | /v1/states/:state/:date.json   |
| /states?state=:state                  | /v1/states/:state/current.json |
| /us?date=date                         | /v1/us/:date.json              |
| /us/daily?date=date                   | /v1/us/:date.json              |
| /v1/us.json                           | /v1/us/current.json            |
| /v1/states.json                       | /v1/states/current.json        |
| /states/info                          | /v1/states/info.json           |
| /states/daily                         | /v1/states/daily.json          |
| /states.json                          | /v1/states/current.json        |
| /states                               | /v1/states/current.json        |
| /us                                   | /v1/us/current.json            |
| /us.csv                               | /v1/us/current.csv             |
| /us/daily                             | /v1/us/daily.json              |

### New API domain name

**Posted August 5, 2020**

In order to serve the API more efficiently, we are moving the API service to a new domain: **api.covidtracking.com**. All of the relative URL paths like `/v1/states/info.json` are exactly the same and unchanged.

You can move your apps to the new domain now. On August 17, we will start redirecting all traffic from our old API endpoints at `covidtracking.com/api` to the new domain.

### Comment on our proposal for a new API

**Posted July 16, 2020**

The COVID Tracking Project was founded in the early days of the COVID pandemic arriving in the US, and provided an API from day one. Since then, the data we collect has undergone many changes.

Because of this, we are working on a new version of the API. Please [read the RFC and give a comment or thumbs up](https://github.com/COVID19Tracking/website/issues/1277). We'd love to hear your feedback!
