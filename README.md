require(data.table)
require(tidyverse)
require(gtools)

setwd("D:/SURESH/DUMP/TDS & NON TDS/")

#unzip("Zip folder workings.zip",exdir = "C:/Users/sf00267/Desktop/Zip folder workings/")
#work = read_csv(unz("Zip folder workings.zip","01-04-2024.csv"),
#                col_names = TRUE,col_types = "c")
ziped_file = unzip("TDS Nov-21 to Aug-24.zip")
ziped_file = lapply(ziped_file,gsub,pattern = "^[.]|[/]",replacement = "") %>% unlist()
require(readr)
Sys.time()
df = sapply(ziped_file,function(x){
  read_csv(unz("TDS Nov-21 to Aug-24.zip",x),
           col_names = TRUE,col_types = "c")
},simplify = F)
Sys.time()
df = rbindlist(l=df,idcol = "File_name",fill = T)
