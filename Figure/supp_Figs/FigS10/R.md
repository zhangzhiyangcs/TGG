```{r}
library(tidyr)
library(dplyr)
data <- read.table("./02.Pan-Genome/06.annotation/Tomato_46genomes.gene.stats.tsv",header=F,sep="\t")
colnames(data) <- c("Name","Group","Stats","Number")
head(data)

newdata <- spread(data,Stats,Number)
write.table(newdata,file="./02.Pan-Genome/06.annotation/Tomato_46genomes.gene.stats_long.xls",sep="\t",quote=F)
plotdata <- filter(data,Stats=="Mean exon size" | Stats == "Mean gene locus size (first to last exon)" | Stats == "Mean number of distinct exons per gene" | Stats == "Mean transcript size (UTR CDS)" | Stats == "Number of genes")
plotdata$Stats <- gsub("Mean gene locus size (first to last exon)","Mean gene locus size",plotdata$Stats)
plotdata$Stats <- gsub("Mean transcript size (UTR CDS)","Mean transcript size",plotdata$Stats)
my_order <- read.table("./02.Pan-Genome/06.annotation/busco.order",header=F)
plotdata$Name <- factor(plotdata$Name,levels=my_order$V1)
plotdata$Number <- as.numeric(plotdata$Number)

ggplot(plotdata)+
  geom_bar(stat="identity",aes(x=Name,y=Number,fill=Group))+
  facet_wrap(~Stats,ncol = 1,scales = "free_y")+
  theme_bw()+
  theme(
    axis.text.x  = element_text(size=6,color="black",angle=90),
    axis.text.y  = element_text(size=6,color="black")
  )+
  scale_fill_manual(values=mypal)+
  scale_y_continuous(breaks = scales::pretty_breaks(3), limits = c(0, NA))

ggsave("./02.Pan-Genome/06.annotation/Tomato-46genomes-gene.stats.pdf",width=7,
       height=7*0.618,units="in")
```