## Two way ANOVA Type I/II/Type III 

## Type I  => #balanced
#Two-way ANOVA with 2 main effects
res.aov2 <- aov(prejudice ~ suffering + liedetection)
summary(res.aov2)

#Two-way ANOVA with interaction effect
#These two calls are equivalent
res.aov3 <- aov(prejudice ~ suffering * liedetection)
res.aov3 <- aov(prejudice ~ suffering + liedetection + suffering:liedetection)
summary(res.aov3)

## Type II  => to test the main effects without interaction significant
#4. Anova
#4.1 Balanced?   看每组被试数
table(liedetection, suffering)  

#4.2 Design is unbalanced, so type II is the way to go!
#install.packages("car")
library(car)
mod1<-lm(prejudice ~ suffering * liedetection)
Anova(mod1,type = "II")
summary(mod1)

#ANOVA results: statistically insignificant main effects and interaction effect.

## Type III SS => to test the main effects with interaction significant

model_III <- lm(gamble~Income*sex,data = Teengamb)
typeIII <- Anova(model_III, type=3)

# 多重比较
##within sex contrasts (look at income, controling for sex)
lsm = lsmeans(model_III, pairwise ~ sex|Income,adjust="tukey")
