# SH-Homework-3.0
plot(myCPM[,2],countdata[,2])
plot(myCPM[,2],countdata[,2],ylim=c(0,50),xlim=c(0,3))
abline(v=0.5,col="blue")
abline(h=10,col="blue")

sampleinfo <- read.delim("data/SampleInfo_Corrected.txt")
par(mfrow=c(1,1))
col.virgin <- c("orange")
col.pregnant <- c("purple")
col.lactate <- c("red")
pch.basal <- c("1")
pch.luminal <- c("4")
pch.celltype <- c("1","4")[sampleinfo$CellType] col.status <- c("red","orange","purple")[sampleinfo$Status]
plotMDS(y,col=col.status,pch=c(1,1,1,1,1,1,4,4,4,4,4,4))
legend("topleft",fill=c("red","purple","orange"),legend=levels(sampleinfo$Status),cex=0.8)
legend("bottom",legend=levels(sampleinfo$CellType),pch=c(1,4))

var_genes <- apply(logcounts, 1, var)
head(var_genes)
select_var <- names(sort(var_genes,decreasing=FALSE))[1:500]
head(select_var)
least_variable_lcpm <- logcounts[select_var,]
dim(least_variable_lcpm)
head(least_variable_lcpm)

mypallete <- brewer.pal(11,"PiYG")
morecols <- colorRampPalette(mypalette)
col.cell <- c("green","red")[sampleinfo$CellType]
heatmap.2(highly_variable_lcpm,col=rev(morecols(50)),trace="none",main="Top 500 least variable genes across samples",ColSideColors=col.cell,scale="row")