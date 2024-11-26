# Teste da API Restful-Booker

## Sumário
1. [Introdução](#introdução)  
2. [Cenários Testados](#cenários-testados)  
    2.1 [Autenticação](#autenticação)  
    2.2 [Gestão de Reservas](#gestão-de-reservas)  
    2.3 [Filtros e Buscas](#filtros-e-buscas)  
3. [Resultados Obtidos](#resultados-obtidos)  
4. [Bugs Encontrados](#bugs-encontrados)  

---

## 1. Introdução
Este documento apresenta os testes realizados na API Restful-Booker, uma plataforma para gestão de reservas de hotel. O objetivo dos testes é validar os principais endpoints e identificar possíveis falhas antes da integração com o front-end.

### Ferramentas Utilizadas
- **Postman**: Para criar e executar os requests.
- **Variáveis de Ambiente**: Configuradas para facilitar a execução dos testes.

---

## 2. Cenários Testados

### 2.1 Autenticação
#### 2.1.1 Gerar Token de Autenticação
- **Request:** `POST https://restful-booker.herokuapp.com/auth`
- **Entrada:** {
    "username" : "admin",
    "password" : "password123"
}
- **Saída Esperada:** Código HTTP 200 e "token": "fc8db8c0908049d".

#### 2.1.2 Tentar Gerar Token com Credenciais Inválidas
- **Request:** `POST https://restful-booker.herokuapp.com/auth`
- **Entrada:** {
    "username" : "admin",
    "password" : "password1232"
}
- **Saída Esperada:** Código HTTP 200 e mensagem "reason": "Bad credentials".

---

### 2.2 Gestão de Reservas
#### 2.2.1 Criar uma Nova Reserva
- **Request:** `POST https://restful-booker.herokuapp.com/booking`
- **Entrada:** {
    "firstname" : "Carolina",
    "lastname" : "Etcheverria",
    "totalprice" : 123,
    "depositpaid" : true,
    "bookingdates" : {
        "checkin" : "2024-11-25",
        "checkout" : "2024-11-28"
    },
    "additionalneeds" : "Breakfast"
}
- **Saída Esperada:** Código HTTP 200 e detalhes da reserva criada.

#### 2.2.2 Buscar uma Reserva Específica
- **Request:** `GET /booking/{id}`
- **Entrada:** ID de uma reserva existente '1514'.
- **Saída Esperada:** Código HTTP 200 e detalhes da reserva.

#### 2.2.3 Listar Todas as Reservas
- **Request:** `GET https://restful-booker.herokuapp.com/booking`
- **Entrada:** Nenhum parâmetro.
- **Saída Esperada:** Código HTTP 200 e lista de reservas.

#### 2.2.4 Atualizar uma Reserva Existente
- **Request:** `PUT https://restful-booker.herokuapp.com/booking/:id`
- **Entrada:** ID de uma reserva existente '1514'.
- **Saída Esperada:** Código HTTP 200 e dados da reserva atualizados.

#### 2.2.5 Deletar uma Reserva
- **Request:** `DELETE https://restful-booker.herokuapp.com/booking/1`
- **Entrada:** ID de uma reserva existente '1514'.
- **Saída Esperada:** Código HTTP 201 indicando sucesso.

---

### 2.3 Filtros e Buscas
#### 2.3.1 Buscar Reservas por Nome
- **Request:** `GET curl -i https://restful-booker.herokuapp.com/booking?firstname=sally&lastname=brown`
- **Entrada:** https://restful-booker.herokuapp.com/booking?firstname=Carolina&lastname=Etcheverria
- **Saída Esperada:** Código HTTP 200 e lista de reservas filtradas.

#### 2.3.2 Buscar Reservas por Data de Check-in
- **Request:** `curl -i https://restful-booker.herokuapp.com/booking?checkin=2014-03-13
`
- **Entrada:** https://restful-booker.herokuapp.com/booking?checkin=2024-11-24
- **Saída Esperada:** Código HTTP 200 e reservas filtradas.

#### 2.3.3 Buscar Reservas por Data de Check-out
- **Request:** `GET curl -i https://restful-booker.herokuapp.com/booking?checkout=2014-05-21`
- **Entrada:** https://restful-booker.herokuapp.com/booking?checkout=2024-11-28
- **Saída Esperada:** Código HTTP 200 e reservas filtradas.

---

## 3. Resultados Obtidos
| Cenário                         | Código HTTP | Comportamento Esperado | Comportamento Observado | Status  |
|---------------------------------|-------------|-------------------------|------------------------|---------|
| Gerar Token de Autenticação     | 200         | Retorna token válido    | Conforme esperado      | ✅       |
| Token com Credenciais Inválidas | 200         | Retorna mensagem de erro| Conforme esperado      | ✅       |
| Criar Nova Reserva              | 200         | Reserva criada          | Conforme esperado      | ✅       |
| Buscar Reserva por ID           | 200         | Detalhes da reserva     | Conforme esperado      | ✅       |
| Listar Todas as Reservas        | 200         | Lista de reservas       | Conforme esperado      | ✅       |
| Atualizar Reserva               | 200         | Reserva atualizada      | Conforme esperado      | ✅        |
| Deletar Reserva                 | 200         | Reserva deletada        | Conforme esperado      | ✅        |
| Filtros por Nome                | 200         | Reservas filtradas      |  Conforme esperado      | ✅      |
| Filtros por Check-in            | 200         | Reservas filtradas      | Conforme esperado      | ✅       |
| Filtros por Check-out           | 200         | Reservas filtradas      | Conforme esperado      | ✅       |

---

## 4. Bugs Encontrados

Nenhum Bug encontrado.


---

**Autor:** Carolina Magalhaes Etcheverria  
**Data:** 26/11/2024
