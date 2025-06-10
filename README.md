# 🛡️ Batalha Naval em Java (TCP/IP)

Este projeto implementa o clássico jogo **Batalha Naval** usando **Java** e **sockets TCP**, permitindo que dois jogadores joguem remotamente, conectando-se ao mesmo servidor.

## 🚀 Visão Geral

O programa é composto por:

- **Servidor:** `ServidorBatalhaNaval.java` (controla a lógica do jogo)
- **Cliente:** `ClienteBatalhaNaval.java` (cada jogador usa um cliente)

---

## 📋 Regras do Jogo

- Tabuleiro 5x5
- Cada jogador posiciona **3 navios**
- O jogo segue turnos alternados
- Vence quem destruir todos os navios do oponente

---

## ⚙️ Como Funciona o Código

### 🔐 Constantes e Variáveis Globais

```java
private static final int PORTA = 4444;
private static final int TAMANHO = 5;
private static final int NAVIOS = 3;
```

Define a porta TCP do servidor e o tamanho do tabuleiro (5x5) com 3 navios por jogador.

---

### 📆 Estrutura dos Tabuleiros

```java
private static char[][] tabuleiro1 = new char[TAMANHO][TAMANHO];
private static char[][] tabuleiro2 = new char[TAMANHO][TAMANHO];
```

Dois tabuleiros independentes: um para cada jogador.

---

### 🧱 Inicialização dos Tabuleiros

```java
private static void inicializarTabuleiro(char[][] tabuleiro) {
    // Preenche o tabuleiro com '-' (água)
}
```

Todos os espaços são inicializados como `'-'`, representando água.

---

### 🚢 Posicionamento dos Navios

```java
private static void posicionarNavios(...)
```

Cada jogador escolhe 3 posições digitando "linha coluna". O servidor valida:

- Se está dentro dos limites
- Se já tem navio naquela posição

Se válido, posiciona com `'N'`.

---

### 🗽 Exibir o Tabuleiro

```java
private static String exibirTabuleiro(char[][] tabuleiro, boolean ocultarNavios)
```

Mostra o tabuleiro ao jogador. O parâmetro `ocultarNavios` esconde os navios inimigos durante o jogo.

---

### ✅ Verificação de Posição

```java
private static boolean isPosicaoValida(int linha, int coluna)
```

Garante que a posição digitada esteja dentro do tabuleiro.

---

### 💥 Ataque

```java
private static boolean processarAtaque(int linha, int coluna, char[][] tabuleiro)
```

- Se for `'N'`: acerta um navio → marca com `'X'`
- Se for `'-'`: erra → marca com `'O'`
- Posições já atacadas são ignoradas

---

### 🏁 Verificação de Vitória

```java
private static boolean venceu(char[][] tabuleiro)
```

Verifica se ainda existe algum `'N'` (navio) no tabuleiro. Se não houver → jogador venceu.

---

### 🧠 Lógica Principal – `main()`

```java
public static void main(String[] args)
```

1. Cria o `ServerSocket`
2. Espera dois jogadores se conectarem
3. Inicializa e envia tabuleiros
4. Cada jogador posiciona seus navios
5. Loop do jogo:
   - Alterna turnos
   - Lê posição de ataque
   - Informa resultado (acerto/erro)
   - Atualiza tabuleiros
6. Se um jogador vencer, envia a mensagem de fim de jogo
7. Fecha todas as conexões

---

## 📱 Comunicação TCP

Cada jogador se conecta ao servidor via socket:

```java
Socket jogador1 = servidor.accept();
BufferedReader in1 = new BufferedReader(...);
PrintStream out1 = new PrintStream(...);
```

O servidor troca mensagens com os jogadores através desses streams.

---

## 🛠️ Como Rodar

1. Compile os arquivos:

```bash
javac ServidorBatalhaNaval.java ClienteBatalhaNaval.java
```

2. Em um terminal, rode o servidor:

```bash
java ServidorBatalhaNaval
```

3. Em dois terminais separados (ou dois computadores), execute os clientes:

```bash
java ClienteBatalhaNaval
```

---

## 🎮 Como Jogar

- Digite a posição dos seus 3 navios no formato:

  ```
  linha coluna
  ```

- Durante o jogo, você ataca da mesma forma:

  ```
  2 3
  ```

- O jogo termina quando um dos jogadores afunda todos os navios do outro.

---

## 📌 Observações

- O jogo foi implementado com foco didático, utilizando apenas bibliotecas padrão do Java.
- É possível expandir o projeto com:
  - Interface gráfica (Swing, JavaFX)
  - Jogar contra IA
  - Log de partidas

---

## 📄 Licença

Este projeto é livre para fins educacionais. Se for usar ou modificar, sinta-se à vontade para dar os créditos. 😄

