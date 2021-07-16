# Practical-Computing
just trials


próby 2 

**You can call out code or a command within a sentence with single backticks. The text within the backticks will not be formatted**
__You can call out code or a command within a sentence with single backticks. The text within the backticks will not be formatted__
You can call out code or a command within a sentence with single backticks. The text within the backticks will not be formatted

library(ggplot2)
library(tidyverse)

data_chol <- read.table('https://raw.githubusercontent.com/wbabik/Practical_computing/teaching/Class_10/data/Cholesterol_Age_R.csv',
                        sep = ';', header = T,
                        stringsAsFactors = T)

head(data_chol)

summ <- tibble(Age = levels(data_chol$AgeGroup),
               mean = by(data_chol$After8weeks, data_chol$AgeGroup, mean, na.rm = T),
               se = by(data_chol$After8weeks, data_chol$AgeGroup,
                       function(x) sd(x, na.rm = T)/sqrt(length(x))))

myplot <- ggplot(data = summ, mapping = aes(x = Age, y = mean,
                                            ymin = mean-se, ymax = mean+se)) +
  geom_bar(stat = 'identity', fill = 'white', colour = 'black') +
  geom_errorbar(width = 0.5) +
  theme_classic() +
  theme(text = element_text(size = 20)) +
  labs(y = "Cholesterol conc. after 8 weeks") +
  scale_x_discrete(limits = c('Young', 'Middle', 'Old'))

myplot
