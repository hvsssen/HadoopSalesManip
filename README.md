cd .\enit_tp1_wordcount\   
(after adding code java or changing ) mvn clean package
docker cp enit_tp1_wordcount/target/Wordcount2-0.jar namenode:/Wordcount2-0.jar 
docker exec -it namenode hadoop jar /Wordcount2-0.jar tn.enit.tp1.StoreSalesJob input output_store_sales
 docker exec -it namenode hadoop fs -cat /user/root/output_payment2/part-r-00000


