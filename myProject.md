Reproducible Pitch Presentation
========================================================
author: Devi Singh
date:   22-03-2015


========================================================
# Objectives
This presentation has been created  R presentations for
my project to be submitted for data science course
Developing Data Product

The Title of my Project is " EMI Calculation " 

# Scope of the project

Almost all over the world banks/financial institution are lending to
general public for construction/purchasing of real estate or any other
items. 

==================================================================== 
To calculate the EMI (equated Montly Installment), I have devloped 
application available on link https://thakurds.shinyapps.io/dataProduct/

Application contains following parameters

- Date
- Name of Person
- Principal Amount
- Rate of Interest
- Period
- Rate of Interest (Monthly/Yearly)
- Income Group


========================================================
# Slide With Code (ui.R)


```r
shinyUI(fluidPage(
  titlePanel("EMI Calculation"),
  sidebarLayout(
    sidebarPanel(
      
  dateInput("date",label = " Date ",value = ""),
  textInput("name", label =" Your Name ",value = "") ,
  numericInput("Pamount", label = "Principal ",value = 10000),
  
  numericInput("RoI", label = "Rate of Interest", value = 10),
  numericInput("Period", label = "Period", value = 10),
  radioButtons("RType", label = "RoI Monthly/Yearly ",  choices = list("Monthly" = 1, "Yearly" = 2
  ),selected = 2),
  checkboxGroupInput("category",label = "Income Group",choices = list("1000-5000" = 1, 
                                      "5001-10000" = 2, "10001-20000" = 3, ">20000"= 4), selected = 1),
  
  br(),
  
  submitButton("Submit")),

  mainPanel(
    textOutput("myEMI")
       
 ))
 ))
```

Slide With server.R
========================================================


```r
library(shiny)

# 
shinyServer(function(input, output) {
  
  output$myEMI <- renderPrint({calculateEMI(input$Pamount, input$RoI/1200, input$Period)})
 
  
})

calculateEMI <- function(amount, eRate, period) {
  return( amount * eRate * (1+eRate)* period /((1+eRate)* period-1))
}
```
