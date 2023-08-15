# telegran-pipeline
## Ingestão de Dados e Armazenamento

Para possibilitar a análise dos dados transacionais provenientes do Telegram, implementamos um sistema de ingestão e armazenamento eficaz. Dado que o Telegram retém as mensagens por apenas 24 horas, optamos por uma abordagem de ingestão via streaming para garantir a coleta contínua e em tempo real dos dados.

### Ingestão via Streaming

Através de um webhook configurado com a API do Telegram, as mensagens recebidas são enviadas diretamente para um serviço de streaming. Esse processo ocorre em tempo real, permitindo que as mensagens sejam capturadas antes de serem perdidas após 24 horas. A ingestão via streaming também garante que as análises sejam sempre atualizadas com os dados mais recentes.

### Armazenamento no AWS S3

As mensagens processadas são armazenadas de forma eficiente no Amazon S3. Optamos por utilizar o formato Parquet devido à sua compressão e eficiência, o que nos permite economizar espaço de armazenamento e melhorar o desempenho das análises subsequentes. Além disso, o Amazon S3 oferece escalabilidade e durabilidade, garantindo que os dados estejam sempre disponíveis e seguros.

### Processo no AWS Lambda

Para realizar a transformação e a escrita das mensagens no formato adequado para armazenamento, criamos uma função AWS Lambda. Esta função é invocada por meio de um endpoint configurado no AWS API Gateway. Ao receber as mensagens do Telegram, a função verifica se elas foram produzidas no grupo especificado, em seguida, as transforma e as escreve no seu formato original JSON em um bucket dedicado no Amazon S3.

### Análise dos Dados

Com as mensagens devidamente armazenadas no Amazon S3, podemos realizar análises de dados avançadas para extrair insights relevantes. Utilizando ferramentas como Amazon Athena, Amazon Redshift ou outras soluções de análise de dados, podemos consultar e visualizar os dados de maneira eficaz, identificando tendências, padrões de comportamento e informações valiosas.

