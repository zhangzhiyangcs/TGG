```{r}
library(tidyr)
library(ggplot2)
library(dplyr)
data1<-read.csv("C:/Users/Younger/Desktop/46_genome_order.txt")
data <- read.table("C:/Users/Younger/Desktop/46genome_RNA_stats.tsv2",header = T)

data$Name<-factor(data$Name,levels=c)


data$Name <- factor(data$Name,levels=rev(my_order))

ggplot(data,aes(x=Name,y=Mapping_rate,fill=Group,order(data[,4])))+
  geom_boxplot()+
  theme_bw()+
  scale_fill_manual(values=mypal)+
  labs(x="",y="83 SRA reads mapping rate")+
  theme(
    legend.position = "top",
    legend.title = element_blank(),
    axis.text.y = element_text(size=6,color="black"),
    axis.text.x=element_text(size=6,color="black",angle=90)
  )

ggsave("C:/Users/Younger/Desktop/46genome_RNA_stats2.pdf",height = 7*0.618+2,width=7,units="in")
```