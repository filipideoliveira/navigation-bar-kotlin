# Checkpoint 1 - Navigation Compose

## Descrição do Projeto

Este projeto consiste em um aplicativo Android desenvolvido com **Jetpack Compose**, cujo objetivo é demonstrar a navegação entre múltiplas telas utilizando o componente **Navigation Compose**.

A aplicação possui telas como Menu, Perfil e Pedidos, permitindo a transição entre elas por meio de rotas, com foco na passagem de parâmetros entre telas e no controle do fluxo de navegação.

---

## Objetivo da Prova

O objetivo deste checkpoint é evoluir um projeto previamente iniciado, aplicando conceitos de navegação no Android com Jetpack Compose, especialmente no que se refere à passagem de parâmetros obrigatórios e opcionais entre telas.

Além da implementação funcional, é necessário demonstrar entendimento técnico sobre como os dados são enviados, recebidos e utilizados dentro das rotas de navegação.

---

## Evoluções Implementadas

### 1. Passagem de parâmetro obrigatório – Tela de Perfil

Inicialmente, a navegação para a tela de perfil não utilizava parâmetros. Foi implementada a passagem de um parâmetro obrigatório (`nome`) através da rota.

A rota foi definida como:

```kotlin
composable(route = "perfil/{nome}")
```

Isso indica que a tela só pode ser acessada se um valor for fornecido para `nome`.

A recuperação do parâmetro é feita utilizando:

```kotlin
val nome: String? = it.arguments?.getString("nome", "Usuário Genérico")
```

E o valor é passado para o composable:

```kotlin
PerfilScreen(..., nome!!)
```

Na navegação, o valor é enviado da seguinte forma:

```kotlin
navController.navigate("perfil/Fulano de Tal")
```

**Explicação:**
O uso de `{nome}` na rota define um parâmetro obrigatório. Caso ele não seja informado, a navegação não funciona corretamente. O uso de `getString()` permite recuperar o valor enviado, e o `!!` garante que o valor não será nulo na execução.

---

### 2. Passagem de parâmetro opcional – Tela de Pedidos

Foi implementado um parâmetro opcional chamado `cliente` na tela de pedidos.

A rota foi definida como:

```kotlin
route = "pedidos?cliente={cliente}"
```

E o argumento configurado com valor padrão:

```kotlin
navArgument("cliente") {
    defaultValue = "Cliente Genérico"
}
```

A recuperação do valor é feita com:

```kotlin
it.arguments?.getString("cliente")
```

E o valor é exibido na tela:

```kotlin
text = "PEDIDOS - $cliente"
```

**Explicação:**
O uso de `?` indica que o parâmetro é opcional. Caso nenhum valor seja enviado, o sistema utiliza automaticamente o `defaultValue`, garantindo que a aplicação não quebre.

---

### 3. Inserção de valor em parâmetro opcional

Após definir o parâmetro opcional, foi implementado o envio de um valor real durante a navegação.

```kotlin
navController.navigate("pedidos?cliente=Cliente XPTO")
```

**Explicação:**
Nesse caso, o valor enviado sobrescreve o `defaultValue`. Isso demonstra como construir dinamicamente a rota e passar dados opcionais de forma controlada.

---

### 4. Passagem de múltiplos parâmetros – Tela de Perfil

A tela de perfil foi evoluída para receber múltiplos parâmetros: `nome` (String) e `idade` (Int).

A nova rota foi definida como:

```kotlin
route = "perfil/{nome}/{idade}"
```

E os argumentos tipados foram configurados:

```kotlin
navArgument("nome") { type = NavType.StringType },
navArgument("idade") { type = NavType.IntType }
```

A recuperação dos valores:

```kotlin
val nome: String? = it.arguments?.getString("nome", "Usuário Genérico")
val idade: Int? = it.arguments?.getInt("idade", 0)
```

Envio dos parâmetros na navegação:

```kotlin
navController.navigate("perfil/Fulano de Tal/27")
```

E exibição na tela:

```kotlin
text = "PERFIL - $nome tem $idade anos"
```

**Explicação:**
Essa abordagem permite a passagem de múltiplos dados entre telas. O uso de `NavType` garante tipagem segura, evitando erros de conversão. A ordem dos parâmetros na rota deve ser respeitada tanto na definição quanto no envio.

---

## Conclusão

As evoluções implementadas demonstram o domínio da navegação entre telas utilizando Jetpack Compose, incluindo o uso de parâmetros obrigatórios, opcionais e múltiplos.

Foi possível compreender não apenas como implementar a navegação, mas também como os dados trafegam entre as telas, garantindo consistência e segurança na aplicação.

O projeto evidencia a capacidade de evolução incremental do código, com integração coerente das novas funcionalidades.
