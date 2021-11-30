```{r cars}
TEpal <- c("#5fc0a7","#abc457","#403dcc","#4771f5",
           "#4da3dc","#f5c456","#ef8b3b","#ec5a29","grey")
mypal <- c(TEpal[6],TEpal[5],TEpal[1])	

data <- read.table("02.Pan-Genome/05.TE/sum_LAI_rename.xls",header=T)
order <- unique(data$Name)
data$Name <- factor(data$Name,levels=order)
ggplot(data,aes(x=Name,y=LAI))+
  geom_boxplot(aes(fill=Group),outlier.size = 0.5)+
  scale_fill_manual(values=mypal)+
  theme_bw()+
  theme(
    axis.text.x=element_text(size=8,color="black",angle=90),
    axis.text.y = element_text(color="black",size=8)
  )+
  ylim(0,60)+
  labs(x="",y="LTR Assembly Index")
ggsave("LAI-Tomato.pdf",height = 7*0.618,width=7,units="in")
```