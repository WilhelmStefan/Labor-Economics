# Project in Labor Economics

### Summary
In their paper "Welfare, the Earned Income Tax Credit, and the Labor Supply of Single Mothers" Bruce D. Meyer and Dan T. Rosenbaum (2001) state that tax and welfare reforms between 1984 and 1996 increased labor supply of single mothers by 6-9%. They used childless single women who were not affected by the reforms as the reference group in a difference-in-difference approach to identify these effects. Based on their finding this projects examines the effects of the subsequent welfare reform on the very same groups. The project provides evidence that the newly introduced TANF (Temporary Assistance for Needy Families) stopped the converging trend of unemployment rates of single mothers and single women. Moreover, it is shown that the TANF benefits have merely a minimal impact on the probability of a single women beeing employed.

## Original paper
### Research Subject
The original paper by Bruce D. Meyer and Dan T. Rosenbaum examined the development of employment rates of single mothers compared to childless single women. They exploited tax and welfare reforms that only affected single mothers but not childless single women. Assuming that employment rates of these two groups would follow the same trend without these interventions they interpreted the change in the difference of employment rate as the causal effect of the tax and welfare reforms.
### Context
Between 1984 and 1996 the US government increased the income tax credit for single mothers significantly. For example, in 1992 the difference in the net income between single mothers and childless single women with a gross yearly income of about 13.000$ amounts to 2.500$. Besides, the welfare benefits for single mothers were changed in a way such that benefits were increased if single mothers had a positiv income and decreased if they were not working at all. Both measures increased incentives for single mothers to get into employment but did not affect childless single women.
### Research strategy
As mentioned before the authors used a difference-in-difference approach stating that employment rates of both groups would follow the same trend without the policy interventions. The change in the difference of empolyment rates of the two groups is interpreted as the causal effect of the policy measures. Furthermore, the authors use a probit regression to quantify the effects of the tax and welfare reforms.
### Results
The employment rate of single mothers increased by 6-9% between 1984 and 1996 in comparison to the employment rate of childless single women. The probit regression revealed that the reduction in income taxes had a significant positve effect on the employment rate of single mothers as well as the welfare reform. A higher income tax credit increases the probability of a single mother beeing employed whereas higher welfare benefits decrease the probability. The authors also state that especially the change in the tax credit and the level of the maximum welfare benefit drive the results.
### Further literature
The findings of Meyer and Rosenbaum are consistent with other research. For example Ellwood (2000) or Jaumotte (2003) provide similar results for the US and other OECD members.

## Own Research
Following the approach of Meyer and Rosenbaum this project investigates the effects of the newly introduced welfare program TANF between 2000 and 2010.
### Data
In research project CPS data recieved from IPUMS (https://cps.ipums.org/cps/) is used. I work with monthly data from 2000 to 2010 including only single women between 19-44 years who are not currently visiting school or who are not able to work. The selection is based on the original paper. Further, I wanted to include the maximum TANF benefit into my analysis which is not included in the CPS data. Therefore, I retrived additional data from the Welfare Rules Database (https://wrd.urban.org/wrd/Query/query.cfm). The data includes the maximum TANF benefit by state depending on the size of the household for the observed time period. The data is then merged by an many-to-one merge command since one oberservation from the benefit data is matched with many observations from the CPS data. The data is merged using the variables state, number of children, year and month.

Stata-Code:
```stata
merge m:1 statefip year month nchild using benefitdata.dat
```

### Context
In 1996 the welfare program investigated by the authors of the original paper was replaced by a welfare program called TANF. Under TANF every state can freely choose the qualification criteria and amount of the welfare benfits. TANF is only granted consecutively for 2 years if the recipient does not work more than 30 hours a week. The lifetime limit for TANF benefits is set to 5 years. Moreover, also childless single women are eligible for TANF. It is striking that the TANF benefits in most states have not been adjusted during the observation time. This leads to a decrease in the average benefit when accounting for inflation. Another noticable observation is the continuous decline in TANF recipients. In 2008 the number of reciepients is almost halved compared to 2000.

**Average TANF Benfits (Inflation adjusted):**

![alt_text](https://github.com/WilhelmStefan/Labor-Economics/blob/main/TANF%20Benefits.png "TANF Benefits")

**Average TANF Recipients:**

|Year|Average Number of Recipients|
|:-------:|-------:|
|2000|1.408.427|
|2001|1.285.527|
|2002|1.221.508|
|2003|1.167.657|
|2004|1.110.821|
|2005|1.024.860|
|2006|930.196|
|2007|837.276|
|2008|799.503|
|2009|-|
|2010|-|
|**Total**|1.087.308|

### Hypotheses
Based on the previous oberservations the following hypotheses are put up:
***The employment rates of childless single women and single mothers will no longer converge but follow the same trend because the benefits are generalised***

***Since benefits are decreasing employment in both groups will rise. The decreasing number of recipients is an indicator for this development***

### Graphical analysis
In order to confirm or reject the hypotheses a graphical analysis is conducted first. I created the variable emp(employed) which equals one if the observed women has been working positve hours last week. Moreover, the same variable is created for the subgroups of childless single women (empsingle) and single mothers (empmother). 
```stata
recode ahrsworkt (999=0) (else=1),gen(emp)
```
```stata
gen empsingle=.
replace empsingle = 0 if emp==0 & nchild == 0
replace empsingle = 1 if emp==1 & nchild == 0
```
```stata
gen empmother=.
replace empmother = 0 if emp==0 & nchild > 0
replace empmother = 1 if emp==1 & nchild > 0
```
Using stata delivers the shown bar diagrams:
```stata
graph bar empsingle empmother, over(year)
```
![alt_text](https://github.com/WilhelmStefan/Labor-Economics/blob/main/Besch%C3%A4ftigung.png "Beschäftigung")



