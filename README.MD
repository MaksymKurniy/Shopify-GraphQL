# 🛒 Shopify GraphQL Queries Collection

Колекція корисних GraphQL запитів та мутацій для роботи з Shopify Admin API через Shopify CLI.

## 📁 Структура репозиторію

```
shopify-graphql/
├── query/              # GraphQL запити (читання даних)
│   └── shop.gql        # Запит інформації про магазин
├── mutation/           # GraphQL мутації (зміна даних)
├── variables/          # JSON файли зі змінними для запитів
├── package.json        # npm скрипти для швидкого виконання
└── README.MD
```

## 🚀 Швидкий старт

### 1. Встановлення Shopify CLI та AI Toolkit

```bash
npm install -g @shopify/cli@latest
```

Перевірка версії:
```bash
shopify version
```

Встановлення AI Toolkit:
https://shopify.dev/docs/apps/build/ai-toolkit

### 2. Авторизація в магазині

Перед виконанням запитів потрібно авторизуватись:

```bash
shopify store auth --store <your-store>.myshopify.com --scopes <scopes>
```

**Приклад:**
```bash
shopify store auth --store my-shop.myshopify.com --scopes read_products,read_orders
```

### 3. Виконання запитів

**З файлу:**
```bash
shopify store execute -s <your-store> --query-file ./query/shop.gql
```

**Inline запит:**
```bash
shopify store execute -s <your-store> --query "{ shop { name } }"
```

**З мутаціями (потребує --allow-mutations):**
```bash
shopify store execute -s <your-store> --query-file ./mutation/example.gql --variable-file ./variables/example.json --allow-mutations
```

## 🔐 Таблиця скоупів (Access Scopes)

### Authenticated Access Scopes (Admin API)

Ці скоупи використовуються для доступу до Admin API від імені користувача.

| Скоуп | Доступ до ресурсів |
|-------|-------------------|
| `read_products`, `write_products` | Product, ProductVariant, Collection, ResourceFeedback, SellingPlan |
| `read_orders`, `write_orders` | AbandonedCheckout, Fulfillment, Order, OrderTransaction |
| `read_all_orders` | Всі замовлення (не лише останні 60 днів) ⚠️ *потребує схвалення* |
| `read_customers`, `write_customers` | Customer, Segment, Company, CompanyLocation |
| `read_inventory`, `write_inventory` | InventoryLevel, InventoryItem |
| `read_locations`, `write_locations` | Location |
| `read_draft_orders`, `write_draft_orders` | DraftOrder |
| `read_content`, `write_content` | Article, Blog, Comment, Page |
| `read_themes`, `write_themes` | OnlineStoreTheme |
| `read_discounts`, `write_discounts` | Discounts features |
| `read_price_rules`, `write_price_rules` | PriceRule |
| `read_gift_cards`, `write_gift_cards` | GiftCard |
| `read_shipping`, `write_shipping` | DeliveryCarrierService |
| `read_fulfillments`, `write_fulfillments` | FulfillmentService |
| `read_metaobjects`, `write_metaobjects` | Metaobject |
| `read_metaobject_definitions`, `write_metaobject_definitions` | MetaobjectDefinition |
| `read_files`, `write_files` | GenericFile |
| `read_translations`, `write_translations` | TranslatableResource, Translation |
| `read_locales`, `write_locales` | ShopLocale |
| `read_markets`, `write_markets` | Market |
| `read_returns`, `write_returns` | Return |
| `read_reports` | Analytics through shopifyqlQuery |
| `read_legal_policies` | ShopPolicy |
| `read_users` | StaffMember (Shopify Plus) |
| `read_shopify_payments_payouts` | ShopifyPaymentsPayout, BalanceTransaction |
| `read_shopify_payments_disputes` | ShopifyPaymentsDispute |

### Fulfillment скоупи

| Скоуп | Опис |
|-------|------|
| `read_assigned_fulfillment_orders`, `write_assigned_fulfillment_orders` | Призначені fulfillment orders |
| `read_merchant_managed_fulfillment_orders`, `write_merchant_managed_fulfillment_orders` | Merchant-managed fulfillments |
| `read_third_party_fulfillment_orders`, `write_third_party_fulfillment_orders` | Third-party fulfillments |
| `read_marketplace_fulfillment_orders` | Marketplace fulfillments |

### Checkout & Payments

| Скоуп | Доступ |
|-------|--------|
| `read_checkout_branding_settings`, `write_checkout_branding_settings` | CheckoutBranding |
| `read_payment_customizations`, `write_payment_customizations` | PaymentCustomization |
| `read_payment_terms`, `write_payment_terms` | PaymentSchedule, PaymentTerms |
| `write_payment_sessions` | PaymentSession (Payments Apps API) |
| `read_delivery_customizations`, `write_delivery_customizations` | DeliveryCustomization |
| `read_cart_transforms`, `write_cart_transforms` | CartTransform |
| `read_validations`, `write_validations` | Validation |

### Web Pixels & Scripts

| Скоуп | Доступ |
|-------|--------|
| `read_customer_events`, `write_pixels` | Web Pixels API |
| `read_script_tags`, `write_script_tags` | ScriptTag |

### Захищені скоупи (потребують схвалення)

| Скоуп | Опис |
|-------|------|
| `read_all_orders` | Доступ до всіх замовлень |
| `read_customer_payment_methods` | Методи оплати клієнтів |
| `read_own_subscription_contracts`, `write_own_subscription_contracts` | Subscription APIs |

---

## 🌐 Unauthenticated Access Scopes (Storefront API)

Для доступу до Storefront API (читання від імені покупця):

| Скоуп | Доступ |
|-------|--------|
| `unauthenticated_read_product_listings` | Product, Collection |
| `unauthenticated_read_product_inventory` | quantityAvailable на ProductVariant |
| `unauthenticated_read_product_tags` | tags на Product |
| `unauthenticated_read_product_pickup_locations` | Location, StoreAvailability |
| `unauthenticated_read_content` | Article, Blog, Comment |
| `unauthenticated_read_checkouts`, `unauthenticated_write_checkouts` | Cart object |
| `unauthenticated_read_customers`, `unauthenticated_write_customers` | Customer object |
| `unauthenticated_read_customer_tags` | tags на Customer |
| `unauthenticated_read_metaobjects` | Metaobject |
| `unauthenticated_read_selling_plans` | Selling plans на Product |

---

## 👤 Customer Access Scopes (Customer Account API)

Для доступу до Customer Account API:

| Скоуп | Доступ |
|-------|--------|
| `customer_read_customers`, `customer_write_customers` | Customer object |
| `customer_read_orders`, `customer_write_orders` | Order object |
| `customer_read_draft_orders` | Draft Order object |
| `customer_read_markets` | Market object |
| `customer_read_metaobjects` | Metaobject |
| `customer_read_companies`, `customer_write_companies` | Company object |
| `customer_read_locations`, `customer_write_locations` | Company Location |
| `customer_read_store_credit_accounts` | Store Credit Account |
| `customer_read_own_subscription_contracts`, `customer_write_own_subscription_contracts` | Subscription Contract |

---

## 💡 Приклади запитів

### Отримати інформацію про магазин

```graphql
# query/shop.gql
query {
  shop {
    name
    email
    primaryDomain {
      url
    }
    currencyCode
    billingAddress {
      city
      country
    }
  }
}
```

**Виконання:**
```bash
shopify store auth --store my-shop.myshopify.com --scopes read_content
shopify store execute --store my-shop.myshopify.com --query-file ./query/shop.gql
```

### Отримати список продуктів

```graphql
# query/products.gql
query {
  products(first: 10) {
    edges {
      node {
        id
        title
        handle
        status
        variants(first: 5) {
          edges {
            node {
              id
              title
              price
              inventoryQuantity
            }
          }
        }
      }
    }
  }
}
```

**Необхідні скоупи:** `read_products`

### Отримати замовлення

```graphql
# query/orders.gql
query {
  orders(first: 10) {
    edges {
      node {
        id
        name
        createdAt
        totalPriceSet {
          shopMoney {
            amount
            currencyCode
          }
        }
        customer {
          email
        }
      }
    }
  }
}
```

**Необхідні скоупи:** `read_orders`

### Оновити продукт (мутація)

```graphql
# mutation/updateProduct.gql
mutation productUpdate($input: ProductInput!) {
  productUpdate(input: $input) {
    product {
      id
      title
    }
    userErrors {
      field
      message
    }
  }
}
```

```json
// variables/updateProduct.json
{
  "input": {
    "id": "gid://shopify/Product/123456789",
    "title": "Оновлена назва продукту"
  }
}
```

**Виконання:**
```bash
shopify store auth --store my-shop.myshopify.com --scopes write_products
shopify store execute --store my-shop.myshopify.com --query-file ./mutation/updateProduct.gql --variable-file ./variables/updateProduct.json --allow-mutations
```

---

## 📋 Корисні команди Shopify CLI

| Команда | Опис |
|---------|------|
| `shopify commands` | Список всіх доступних команд |
| `shopify help [command]` | Довідка по команді |
| `shopify version` | Поточна версія CLI |
| `shopify upgrade` | Оновити CLI до останньої версії |
| `shopify store auth --store <domain> --scopes <scopes>` | Авторизація в магазині |
| `shopify store execute --help` | Довідка по execute |

---

## 📚 Корисні посилання

- [Shopify GraphQL Admin API Reference](https://shopify.dev/docs/api/admin-graphql)
- [Access Scopes Documentation](https://shopify.dev/docs/api/usage/access-scopes)
- [Shopify CLI Documentation](https://shopify.dev/docs/api/shopify-cli)
- [GraphQL Learning Kit](https://shopify.dev/docs/apps/build/graphql)

---

## ⚠️ Важливі обмеження

1. **Мінімальні скоупи** — запитуйте тільки необхідні скоупи для вашого функціоналу
2. **Захищені дані** — деякі скоупи потребують схвалення через Partner Dashboard
3. **60-денне вікно** — за замовчуванням доступні лише замовлення за останні 60 днів
4. **Rate Limits** — Shopify має обмеження на кількість запитів

---

## 🤝 Як додати новий запит

1. Створіть `.gql` файл у відповідній папці (`query/` або `mutation/`)
2. Якщо потрібні змінні — створіть `.json` файл у `variables/`
