# Average Income by Employment type = CALCULATE(AVERAGE('Loan_default'[Income]),ALLEXCEPT('Loan_default','Loan_default'[EmploymentType]))

 # Average loan by Age Group = 
AVERAGEX(VALUES('Loan_default'[Age Groups]),
AVERAGE('Loan_default'[LoanAmount]))

# Default rate by employment type = 
var totalrecords = COUNTROWS(ALL('Loan_default'))
var defaultcases = COUNTROWS(FILTER('Loan_default','Loan_default'[Default]=TRUE()))

RETURN
CALCULATE(DIVIDE(defaultcases,totalrecords),ALLEXCEPT('Loan_default','Loan_default'[EmploymentType])) * 100


# Default Rate by Year = 
Var totalloans = 
          CALCULATE(COUNTROWS('Loan_default'),
          ALLEXCEPT('Loan_default',Loan_default[Year]))

 # VAR default = CALCULATE(COUNTROWS(FILTER('Loan_default','Loan_default'[Default] = TRUE())),ALLEXCEPT('Loan_default',Loan_default[Year]))

RETURN
DIVIDE(default,totalloans)*100

 # Loan Amount by Purpose = SUMX(FILTER('Loan_default',NOT(ISBLANK('Loan_default'[LoanAmount]))),'Loan_default'[LoanAmount])   


# Average loan amount (High credit) = 
AVERAGEX(FILTER('Loan_default','Loan_default'[Credit score Bins]="High"),
'Loan_default'[LoanAmount])

# Loans by Education type = 
COUNTROWS(FILTER('Loan_default',NOT(ISBLANK('Loan_default'[LoanID]))))

 # Median by credit score bins = 
MEDIANX('Loan_default','Loan_default'[LoanAmount])

 # Total loan (Credit Bins) = 
CALCULATE(SUM('Loan_default'[LoanAmount]),'Loan_default'[Age Groups] = "Adults",ALLEXCEPT('Loan_default',
'Loan_default'[Age],'Loan_default'[Age Groups],'Loan_default'[CreditScore],'Loan_default'[Credit score Bins]))


# total loan (middle age adults) = 
SUMX(FILTER('Loan_default','Loan_default'[Age Groups]="Middle Age Adults"),
'Loan_default'[LoanAmount])
