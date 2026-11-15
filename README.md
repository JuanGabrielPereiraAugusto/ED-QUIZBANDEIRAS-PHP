# 🌍 Quiz de Países Pro — Quiz de Bandeiras em PHP

Jogo de perguntas em **PHP** em que o jogador vê a bandeira de um país e precisa adivinhar qual é, entre 4 alternativas, antes que o tempo acabe.

Os dados dos países vêm da API pública **[REST Countries](https://restcountries.com/)**, com nomes em português.

---

## ✨ Funcionalidades

- 🏳️ **Bandeiras reais** de todos os países, carregadas da API REST Countries
- 🔤 **4 alternativas** por pergunta, embaralhadas a cada rodada
- ⏱️ **Cronômetro** por pergunta, que muda de cor quando o tempo está acabando e envia a resposta sozinho ao zerar
- 🎚️ **3 níveis de dificuldade**:

  | Nível | Tempo | Países | Bônus por acerto |
  |---|---|---|---|
  | Fácil | 20 s | Países conhecidos ou com mais de 15 milhões de habitantes | 10 pts |
  | Médio | 15 s | Países conhecidos ou com mais de 3 milhões de habitantes | 15 pts |
  | Difícil | 10 s | Todos os países | 20 pts |

- 🔢 **Quantidade de perguntas** escolhida pelo jogador: 5, 10, 15 ou 20
- 💡 **Botão de dica** que mostra a capital e a região do país da bandeira
- 🧮 **Pontuação** = bônus do nível + segundos que sobraram no cronômetro
- 🔥 **Sequência de acertos** (streak), guardando a melhor da partida
- 📚 **Curiosidades** após cada resposta: capital, região e população do país
- 🏆 **Ranking** com as 10 melhores pontuações (desempate pela maior sequência)
- 💾 **Cache local** da API por 24 horas: o jogo continua funcionando mesmo se a API ficar fora do ar

---

## 🛠️ Tecnologias utilizadas

| Tecnologia | Uso |
|---|---|
| **PHP 8** | Lógica do jogo e sessões |
| **cURL** | Consumo da API (com `file_get_contents` como alternativa) |
| **JSON** | Cache dos países e armazenamento do ranking |
| **JavaScript** | Cronômetro regressivo |
| **CSS** | Estilização da interface |
| **[REST Countries API](https://restcountries.com/)** | Dados e bandeiras dos países |

---

## 📁 Estrutura do projeto

```
ED-QUIZBANDEIRAS-PHP/
├── index.php                # Página principal: início da partida, perguntas, resultado e ranking
├── includes/
│   └── functions.php        # Lógica do jogo: API, cache, dificuldade, perguntas, pontuação e ranking
├── assets/
│   ├── app.js               # Cronômetro das perguntas
│   └── style.css            # Estilos da interface
└── data/
    ├── countries_cache.json # Cache dos países vindos da API (renovado a cada 24 h)
    └── ranking.json         # Top 10 jogadores
```

---

## ⚙️ Como funciona

1. Na primeira execução, o jogo busca os países na API e salva em `data/countries_cache.json`.
2. O jogador escolhe a **dificuldade** e a **quantidade de perguntas**.
3. Os países são filtrados conforme o nível e embaralhados.
4. A cada pergunta, o jogo sorteia 3 países errados para completar as 4 alternativas.
5. O tempo é controlado **no servidor** (pela sessão), então recarregar a página não reinicia o cronômetro.
6. Ao final, o jogador digita o nome (até 24 caracteres) e a pontuação entra no ranking, se estiver entre as 10 melhores.

---

## 🚀 Como executar

### Pré-requisitos
- [XAMPP](https://www.apachefriends.org/) (ou WAMP / Laragon) com **PHP 8+**
- Internet na primeira execução, para baixar os países da API

### Passo a passo
1. Baixe o projeto (**Code → Download ZIP**) e extraia.
2. Copie a pasta para `C:\xampp\htdocs\`.
3. Abra o **XAMPP Control Panel** e clique em **Start** no **Apache**.
4. Verifique se a pasta `data/` tem permissão de escrita (o jogo grava o cache e o ranking nela).
5. Acesse no navegador: `http://localhost/ED-QUIZBANDEIRAS-PHP/`

> Não é necessário banco de dados: tudo é salvo em arquivos JSON.

---

## 🔒 Boas práticas aplicadas

- `declare(strict_types=1)` para tipagem estrita
- Escape de saída com `htmlspecialchars` (função `h()`), contra XSS
- Tempo de resposta validado no servidor, não só no navegador
- Nome do jogador limpo e limitado antes de salvar no ranking
- Ranking salvo apenas uma vez por partida

---

## 👤 Autor

**Juan Gabriel Pereira Augusto**
GitHub: [@JuanGabrielPereiraAugusto](https://github.com/JuanGabrielPereiraAugusto)

Projeto desenvolvido para fins acadêmicos.
