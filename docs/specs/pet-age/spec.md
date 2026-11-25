---
# Pet age on the owner details page

Signal: https://github.com/spring-projects/spring-petclinic/issues/1899 ("Display Pet Age and Species-Specific Age Group"). This spec covers only the age-in-years display from that issue. Species-specific age groups (young, adult, senior) are out of scope.

## Who, pain, why now

Who: clinic staff looking at an owner's page in Spring PetClinic.

Pain: the page already shows each pet's birth date, but not the pet's age in years. Staff have to compute that themselves.

Why now: issue #1899 asks for the pet's age, calculated from today's date, when viewing the pet. The same gap is still present in this fork: the owner details page lists Name, Birth Date, and Type, and Pet has no age method.

## Stories

### 1. Show pet age on the owner details page

Given a pet with a recorded birth date
When I open that pet's owner details page
Then I see an Age line under Birth Date, showing the pet's age in whole years, calculated as `Period.between(birthDate, today).getYears()`

### 2. Leo's age from seed data

Given Leo, George Franklin's cat, born 2010-09-07 (seed data, owner page http://localhost:8080/owners/1)
When I open http://localhost:8080/owners/1 on Nov 25, 2026
Then Leo's Age line shows 16 years

### 3. Missing birth date

Given a pet with no birth date
When I open the owner details page
Then the Age line is omitted or shows that age is unknown, and the page does not error

## What we still do not know

- For a missing birth date, should the Age line be omitted, or should it say that age is unknown?
- Should age also appear anywhere else the birth date is shown, such as the visit form or the owners list? This spec is for the owner details page only.
- Exact label wording (for example, "Age" with the value "16 years").
---
