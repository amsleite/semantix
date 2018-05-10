# semantix
##Desafio Engenheiro de dados



##Qual o objetivo do comando cache em Spark?
O comando cache tem a função de carregar os dados em memória, e deixa-lo disponível para as execuções seguintes. Este comando é útil em operações que utilizem o conjunto de dados repetidamente, assim somente na primeira execução haverá o tempo de consulta e carga em memoria dos dados.

##O mesmo código implementado em Spark é normalmente mais rápido que a implementação equivalente em MapReduce. Por quê?
A implementação do Spark contém otimizações sobre a arquitetura e fluxo de execução, sendo que os principais atributos que ocasionam a melhora de desempenho são : 1.   execução das tarefas em memória, tornando o acesso aos dados mais rápido do que comparados com a busca em disco 2. Otimização da criação de ambientes java entre os nós da rede, agilizando o processo por haver JVM disponíveis 3. Processamento paralelo distribuído com RDD, que garantem a integridade de arquivos em um ambiente de processamento compartilhado 4. Otimização da arquitetura para que em todos os pontos do processamento ocorra em menor tempo possível. Devido a estes adequações, as execuções sem Spark são em modo geral mais rápidas que as em MapReduce.


##Qual é a função do SparkContext?
SparkContext tem a função de criar os serviços necessários para a aplicação Spark como RDDs, accumulators e  broadcast variables ,  e estabelecer a conexão para o ambiente de execução,  assim podendo somente um estar ativo por JVM. Desta forma,  possui a função central dentro de uma aplicação Spark.


##Explique com suas palavras o que é Resilient Distributed Datasets (RDD).
RDD é a estrutura de dados que permite com que o processamento distribuído e em paralelo possa ocorrem sem que haja perda de dados entre os nós de uma rede. O conceito de computação distribuída depende de uma estrutura representada pelo RDD, do qual cria uma estrutura logica para os dados , que permite sua distribuição e  consistência.

##GroupByKey é menos eficiente que reduceByKey em grandes dataset. Por quê?
reduceByKey  possui uma implementação que o torna mais eficiente quando o conjunto de dados demanda um maior poder computacional devido a forma de contagem dos elementos agrupados acontecerem de forma distribuída, e os grupos já sumarizados são calculados em uma etapa posterior sem grande necessidade de processamento robusto.  Desta formas, em grandes datasets é utilizado a capacidade do processamento distribuído para gerar o resultado de agrupamento.


##Explique o que o código Scala abaixo faz. 

val textFile = sc.textFile("hdfs://...") 
// declaração de uma variavel imutavel  “textFile” , sendo atribuido a ela os dados contidos no //HDFS com o uso da função SparkContext
val counts = textFile.flatMap(line => line.split(" "))
// declaração da variável “count” , sendo atribuído a ela os conjuntos de dados separados por //espaço
            .map(word => (word, 1)) 
//mapeamento dos grupos encontrados no dataset
            .reduceByKey(_ + _) 
//agrupamento dos grupos com o uso da implementação reduceByKey
counts.saveAsTextFile("hdfs://...")
//Resultado contendo as palavras do arquivo com a contagem de ocorrências

