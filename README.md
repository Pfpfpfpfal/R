Линейные графики

library(ggplot2)
library(dplyr)

beav <- beav %>% mutate(activ = factor(activ))

ggplot(data = beav, aes(x = id, y = temp, group = activ, color = activ)) +
  geom_line() + geom_point() +
  scale_color_manual(values = c("red", "blue"),                    
                     labels = c("Not active", "Active")) + 
  labs(title = "Beavers: body temperature", 
       x = "Observations", 
       y = "Temperature, C") +
  theme_bw()

  Гистограммы

library(ggplot2)
library(dplyr)

beav <- beav %>% mutate(activ = factor(activ))

ggplot(data = beav, aes(x = temp)) +
  geom_histogram(binwidth = 0.1,
                 fill = "yellowgreen", 
                 color = "black") + 
  geom_vline(xintercept = median(beav$temp), 
             color = "red",
             lty = 2)+ 
  geom_hline(yintercept = 15, color = "red")

Гистограмма по группам

library(ggplot2)
library(dplyr)

beav <- beav %>% mutate(activ = factor(activ))

ggplot(data = beav, aes(x = temp, group = activ, fill = activ)) +
  geom_histogram()

Гистограмма с наложением

library(ggplot2)
library(dplyr)

beav <- beav %>% mutate(activ = factor(activ))

ggplot(data = beav, aes(x = temp, group = activ, fill = activ)) +
  geom_density(alpha = 0.5) + geom_rug()

Вариант 2

Ящики с усами

library(ggplot2)
library(dplyr)

beav <- beav %>% mutate(activ = factor(activ))

ggplot(data = beav, aes(y = temp)) +
  geom_boxplot()

По группам

library(ggplot2)
library(dplyr)

beav <- beav %>% mutate(activ = factor(activ))

ggplot(data = beav, aes(x = "", y = temp, group = activ, fill = activ)) +
  geom_boxplot()

Скрипичные диаграммы

library(ggplot2)
library(dplyr)

beav <- beav %>% mutate(activ = factor(activ))

ggplot(data = beav, aes(x = "", y = temp, group = activ, fill = activ)) +
  geom_violin()

  Диаграммы рассеивания

library(ggplot2)
library(dplyr)

dat <- read.csv("https://raw.githubusercontent.com/allatambov/R-programming-3/master/lectures/lect9-02-02/wgi_fh_new.csv", dec = ",")
dat <- na.omit(dat)

ggplot(data = dat, aes(x = va, y = rl)) +
  geom_point() + 
  labs(title = "WGI indicators", 
       x = "Voice and Accountability", 
       y = "Rule of Law") + 
  geom_smooth()

Bubble plot

library(ggplot2)
library(dplyr)

dat <- read.csv("https://raw.githubusercontent.com/allatambov/R-programming-3/master/lectures/lect9-02-02/wgi_fh_new.csv", dec = ",")
dat <- na.omit(dat)

ggplot(data = dat, aes(x = va, y = rl)) +
  geom_point(aes(size = fh), color = "cornflowerblue") + 
  labs(title = "WGI indicators", 
       x = "Voice and Accountability", 
       y = "Rule of Law") 

Дополнение

library(ggplot2)
library(dplyr)

dat <- read.csv("https://raw.githubusercontent.com/allatambov/R-programming-3/master/lectures/lect9-02-02/wgi_fh_new.csv", dec = ",")
dat <- dat %>% mutate(not_free = as.integer(fh >= 5.5),
                      partly_free = as.integer(fh >= 3 & fh <= 5),
                      free = as.integer(fh <= 2.5))

colnames(dat)[11] <- "fh_score"

dat$fh_type <- names(dat[12:14])[max.col(dat[12:14])]
dat$fh_type <- factor(dat$fh_type)

ggplot(data = dat, aes(x = va, y = rl)) +
  geom_point(aes(size = fh_score, color = fh_type)) + 
  labs(title = "WGI indicators", x = "Voice and Accountability", 
       y = "Rule of Law") 

По группам

library(ggplot2)
library(dplyr)

dat <- read.csv("https://raw.githubusercontent.com/allatambov/R-programming-3/master/lectures/lect9-02-02/wgi_fh_new.csv", dec = ",")
dat <- dat %>% mutate(not_free = as.integer(fh >= 5.5),
                      partly_free = as.integer(fh >= 3 & fh <= 5),
                      free = as.integer(fh <= 2.5))

colnames(dat)[11] <- "fh_score"

dat$fh_type <- names(dat[12:14])[max.col(dat[12:14])]
dat$fh_type <- factor(dat$fh_type)

ggplot(data = dat, aes(x = va, y = rl)) +
  geom_point() + 
  labs(title = "WGI indicators", 
       x = "Voice and Accountability", 
       y = "Rule of Law") + 
  facet_wrap(~fh_type)
