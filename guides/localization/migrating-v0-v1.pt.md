# Migração da versão 0 para versão 1 da API de Pagamentos do Mercado Pago

No Mercado Pago procuramos sempre otimizar nossa plataforma oferecendo a mais alta eficiência e segurança no processamento de pagamentos.

No momento, estamos trabalhando na migração da nossa API  versão 0 para a versão 1 com o objetivo de manter os mais altos padrões de qualidade.

Consequentemente a versã 0 vai parar de ter suporte a partir de 10 de dezembro de 2018.
 

### Pontos para serem levados em conta

* A alteração terá impacto **a partir de 10 de dezembro de 2018.**
* Se você usa apenas os botões de pagamento de Mercado Pago, essa alteração não afetará você.
* Se você usa apenas Mercado Shops, essa alteração não afetará você.
* Caso tenha seu **próprio e-commerce, consulte sua equipe de TI**.
* Caso **opere com alguma plataforma de e-commerce**, como por exemplo: Magento, Shopify ou outros **Consulte seu respectivo suporte técnico**.

## Recursos migrados

A tabela abaixo traz uma relação dos recursos migrados.

| Uso                      | Método | URI do Recurso deprecado               | URI do Recurso equivalente       | Referência                                                      |
|--------------------------|--------|----------------------------------------|----------------------------------|-----------------------------------------------------------------|
| Devoluções               | `POST` | /collections/$payment_id/refunds       | /v1/payments/$payment_id/refunds |-                                                                |
| Devoluções               | `PUT`  | /collections/$payment_id               | /v1/payments/$payment_id/        |[acesse](https://www.mercadopago.com.br/developers/pt/reference/payments/_payments_id/put/)	 |
| Atualização de pagamento | `PUT`  | /payments/$payment_id                  | /v1/payments/$payment_id/        |[acesse](https://www.mercadopago.com.br/developers/pt/reference/payments/_payments_id/put/)    |
| Atualização de pagamento | `PUT`  | /collections/$payment_id               | /v1/payments/$payment_id/        |[acesse](https://www.mercadopago.com.br/developers/pt/reference/payments/_payments_id/put/)    |
| Pagamentos               | `GET`  | /payments/$payment_id                  | /v1/payments/$payment_id/        |[acesse](https://www.mercadopago.com.br/developers/pt/reference/payments/_payments_id/get)    |
| Pagamentos               | `GET`  | /collections/$payment_id               | /v1/payments/$payment_id/        |[acesse](https://www.mercadopago.com.br/developers/pt/reference/payments/_payments_id/get)    |
| Notificação de pagamentos| `GET`  | /collections/notifications/$payment_id | /v1/payments/$payment_id/        |[acesse](https://www.mercadopago.com.br/developers/pt/reference/payments/_payments_id/get)    |
| Busca de pagamentos      | `GET`  | /payments/search                       | /v1/payments/search              |[acesse](https://www.mercadopago.com.br/developers/pt/reference/payments/_payments_search/get)|
| Busca de pagamentos      | `GET`  | /collections/search                    | /v1/payments/search              |[acesse](https://www.mercadopago.com.br/developers/pt/reference/payments/_payments_search/get)|

### Exemplos

#### Pesquisar por pagamentos

Para a busca de pagamentos o recurso /v1/payments/search deve ser utilizado levando em conta que o resultado desta pesquisa retornará os pagamentos como pagador e coletor do invocador.

Para manter a consistência semântica com os resultados do recurso /payments/search, você deve adicionar o parâmetro payer.id com seu ID de usuário.

```json
curl -X GET \
 "http://api.mercadopago.com/v1/payments/search?access_token=ENV_ACCESS_TOKEN&site_id=MLA&limit=50&range=date_created&end_date=NOW&begin_date=NOW-90DAYS&sort=date_created&criteria=desc&payer.id=PAYER_ID" 
```

Para manter a consistência semântica com os resultados do recurso /collections/search, você deve incluir o parâmetro collector.id com seu ID do usuário.

```json
curl -X GET \
 "http://api.mercadopago.com/v1/payments/search?access_token=ENV_ACCESS_TOKEN&site_id=MLA&limit=50&range=date_created&end_date=NOW&begin_date=NOW-90DAYS&sort=date_created&criteria=desc&collector.id=COLLECTOR_ID" 
```

#### Devolução Total
```json
curl -X POST \
        -H "content-type: application/json" \
        "https://api.mercadopago.com/v1/payments/:id/refunds?access_token=ENV_ACCESS_TOKEN"
```

#### Devolução Parcial

```curl
curl -X POST \
        -H 'content-type: application/json' \
        'https://api.mercadopago.com/v1/payments/12861583/refunds?access_token=ENV_ACCESS_TOKEN' \
        -d '{
                "amount": 5.0
        }'
```

Caso você precise fazer adaptações, **é importante que você se lembre de fazer essa alteração em tempo hábil.**

Se você tiver alguma dúvida ou precisar de ajuda para concluir com êxito essa mudança, entre em contato conosco através do seguinte [formulário de contato](https://www.mercadopago.com.br/developers/pt/support).

Equipe do Mercado Pago.
