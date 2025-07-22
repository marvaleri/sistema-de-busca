# 🔍 Sistema de Busca em Catálogo de Produtos em Rust

Este projeto é uma aplicação de terminal escrita em Rust que permite buscar produtos em um catálogo com suporte a acentuação e caching. A aplicação normaliza os termos de busca e os nomes dos produtos para facilitar a correspondência, melhorando a experiência do usuário.

<br>

# 📦 Funcionalidades

- ✅ Busca por nome de produto (ignora acentos e capitalização)
- ✅ Cache de buscas para acelerar consultas repetidas
- ✅ Exibição de todos os produtos cadastrados
- ✅ Testes automatizados para validação das funcionalidades principais

<br>

# 🧱 Estrutura do Projeto

`src/` <br>
`├── main.rs           # Código principal da aplicação` <br>
`├── products.rs       # Definição da struct Product e função de criação do catálogo` <br>
`Cargo.toml            # Arquivo de configuração do projeto Rust` <br>

<br>

# 🧠 Como funciona
- **Normalização:** A função preprocess remove acentos e caracteres especiais, mantendo apenas letras e números em minúsculas. <br>
- **Busca:** Compara o termo normalizado com os nomes dos produtos no catálogo. <br>
- **Cache:** Armazena os resultados da busca para que repetições sejam mais rápidas. <br>
- **Testes:** Funções de teste garantem que o processamento e a busca funcionem corretamente.<br>

<br>

# 🧮 Estruturas de Dados Utilizadas

`struct Product`	Representa um produto, com campos `id: u32`, `name: String`, `category: String`.

`HashMap<u32, Product>`	Tabela principal de produtos, onde a chave é o ID e o valor é o `Product`.

`HashMap<String, Vec<u32>>`	Cache de busca, onde a chave é o termo normalizado e o valor são os IDs dos produtos encontrados.

`Vec<&Product>`	Lista temporária dos produtos que correspondem ao termo buscado.

`String`	Usado para armazenar entradas e termos normalizados.

<br>

# ▶️ Como executar
1. Clone o repositório
~~~
git clone https://github.com/marvaleri/catalogo-produtos-rust.git
cd catalogo-produtos-rust
~~~

2. Compile e execute
Certifique-se de que o Rust está instalado.
~~~
cargo run
~~~

3. Execute os testes
~~~~
cargo test
~~~~

# 🛠️ Dependências
`unicode-normalization:` Usada para remover acentuação dos textos. <br>
`Biblioteca padrão do Rust (std):` manipulação de I/O, tempo, strings e coleções.

<br>

# 🧪 Testes incluídos
🧪 Normalização de texto (`preprocess`) <br>
🧪 Busca por nome <br>
🧪 Cache funcionando corretamente <br>
🧪 Casos onde nenhum produto é encontrado <br>

<br>

# 📈 Considerações sobre Desempenho e Escalabilidade
`Cache de busca:` A utilização de `HashMap<String, Vec<u32>>` como cache reduz drasticamente o tempo de resposta para buscas repetidas, tornando a aplicação mais responsiva ao longo do tempo.

`Busca linear:` A filtragem de produtos é feita por uma busca linear (`filter`) em todos os produtos do `HashMap`, o que funciona bem para catálogos pequenos ou médios. Para grandes volumes, isso se tornaria um gargalo.

`Pré-processamento leve:` A normalização de texto com `unicode-normalization` é relativamente eficiente, mas poderia ser substituída ou otimizada para grandes volumes de dados com técnicas mais especializadas ou armazenando versões normalizadas dos nomes dos produtos.

**Escalabilidade futura** <br>
Para grandes catálogos (milhares ou milhões de itens), considere:<br>
- Indexação com estruturas como tries ou inverted indices.
- Persistência em banco de dados com suporte a buscas textuais (ex: PostgreSQL com `pg_trgm` ou ElasticSearch).
- Threads ou async I/O para paralelizar operações.
