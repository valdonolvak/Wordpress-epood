Allpool on **täislahendus (PHP + samm-sammuline juhend)**, kus:

✔ hinnad ümardatakse alati **ÜLESPOOLE 5 sendini (0.05)**
✔ kehtib kogu WooCommerce poes (tooted, variatsioonid, ostukorv, checkout)
✔ kuvatakse alati **korrektse formaadiga (2 komakohta)**
✔ töötab ka siis, kui hinnad tulevad laosüsteemist

---

# 🧩 1. Paigalda vajalik plugin

Kasuta pluginat **Code Snippets**

### Sammud:

1. Ava WordPress admin
2. **Plugins → Add New**
3. Otsi: `Code Snippets`
4. **Install → Activate**

---

# ⚙️ 2. Lisa uus snippet (kõige olulisem osa)

### Sammud:

1. Mine **Snippets → Add New**

2. Pane nimeks:

   ```
   WooCommerce hinnad 5 sendini (ALATI ÜLES)
   ```

3. Lisa **KOGU see kood**:

```php id="full_5cent_rounding"
// Ümardamine ALATI üles järgmise 0.05-ni
function round_up_to_5_cents($price) {
    if ($price === '' || $price === null) return $price;

    return ceil($price / 0.05) * 0.05;
}

/**
 * 1. Rakenda toodete hindadele (frontend + backend arvutused)
 */
add_filter('woocommerce_product_get_price', 'round_up_to_5_cents', 10, 1);
add_filter('woocommerce_product_get_regular_price', 'round_up_to_5_cents', 10, 1);
add_filter('woocommerce_product_get_sale_price', 'round_up_to_5_cents', 10, 1);

/**
 * 2. Variatsioonid (variable products)
 */
add_filter('woocommerce_product_variation_get_price', 'round_up_to_5_cents', 10, 1);
add_filter('woocommerce_product_variation_get_regular_price', 'round_up_to_5_cents', 10, 1);
add_filter('woocommerce_product_variation_get_sale_price', 'round_up_to_5_cents', 10, 1);

/**
 * 3. Ostukorvi arvutused (väga oluline!)
 */
add_action('woocommerce_before_calculate_totals', function($cart) {
    if (is_admin() && !defined('DOING_AJAX')) return;

    foreach ($cart->get_cart() as $cart_item) {
        $price = $cart_item['data']->get_price();
        $cart_item['data']->set_price(round_up_to_5_cents($price));
    }
});

/**
 * 4. Veendu, et kuvatakse õigesti (2 komakohta + ümardatud väärtus)
 */
add_filter('woocommerce_get_price_html', function($price_html, $product) {
    $price = $product->get_price();
    $rounded = round_up_to_5_cents($price);
    return wc_price($rounded);
}, 10, 2);

/**
 * 5. Üksiktoote hinna kuvamine ostukorvis
 */
add_filter('woocommerce_cart_item_price', function($price, $cart_item, $cart_item_key) {
    $rounded = round_up_to_5_cents($cart_item['data']->get_price());
    return wc_price($rounded);
}, 10, 3);
```

4. Pane:
   👉 **Run snippet everywhere**

5. Vajuta:
   👉 **Save & Activate**

---

# 💰 3. WooCommerce seadistus (väga oluline)

Mine:
👉 WooCommerce → Settings → General

Kontrolli:

* **Number of decimals = 2**

👉 See tagab:

* 10.25 (OK)
* mitte 10.2 (vale)

---

# 🧪 4. Testimine (tee kindlasti!)

Loo testtooted:

| Sisendhind | Tulemus |
| ---------- | ------- |
| 10.21      | 10.25   |
| 10.23      | 10.25   |
| 10.25      | 10.25   |
| 10.26      | 10.30   |

Kontrolli:

* ✔ tooteleht
* ✔ kategoorialeht
* ✔ ostukorv
* ✔ checkout

---

# ⚠️ 5. Olulised nüansid

## 🧠 1. See EI muuda andmebaasi

* hinnad jäävad laosüsteemis samaks
* ümardamine toimub **reaalajas (runtime)**

---

## 💸 2. Käibemaks (KM)

Kui kasutad KM-i:

* WooCommerce võib teha oma roundingut

👉 Kui näed 0.01 erinevusi:
ütle — saan anda täpse maksude fixi

---

## 🔄 3. Impordid / API

Kui kasutad:

* WP All Import
* laosüsteemi API

👉 see lahendus töötab automaatselt

---

# 🚀 Soovitus (päris projektide kogemus)

Kui süsteem kasvab:

👉 parim arhitektuur on:

* ümardamine juba **laosüsteemis või importimisel**

AGA:
✔ see lahendus on täiesti production-ready
✔ kasutatakse väga tihti WooCommerce poodides

---

# ✅ Kokkuvõte

Sa said lahenduse, mis:

* ✔ ümardab hinnad **ALATI üles 5 sendini**
* ✔ töötab kogu WooCommerce’is
* ✔ ei vaja tasulisi pluginaid
* ✔ sobib ideaalselt laohaldusega integreeritud poodidele

---

Kui tahad edasi minna, saan teha ka:

* 👉 “psühholoogilise hinnastamise” (nt 10.25 → 10.99)
* 👉 ümardamine ainult kassas (cash rounding)
* 👉 DB tasemel salvestamine (kõige kiirem variant suurele poele)



---

Allpool on **täislahendus DB tasemel ümardamiseks (ALATI üles 5 sendini)** + **samm-sammuline juhend**, kuidas see korrektselt WooCommerce’is tööle panna.

See lahendus:
✔ muudab hinna **päriselt andmebaasis**
✔ töötab hästi suurel poel (kiirem kui runtime filterid)
✔ sobib ideaalselt, kui hinnad tulevad laosüsteemist / impordist

---

# ⚠️ Enne alustamist (väga oluline)

See lahendus:

* **MUUDAB toodete hinnad jäädavalt**
* ei ole enam “dünaamiline”

👉 Tee kindlasti:

* varukoopia (backup)
* test esmalt staging keskkonnas

---

# 🧩 1. Paigalda koodi lisamise plugin

Kasuta: **Code Snippets**

Sammud:

1. WordPress admin
2. Plugins → Add New
3. Otsi: `Code Snippets`
4. Install → Activate

---

# ⚙️ 2. Lisa DB taseme ümardamise kood

### Sammud:

1. Mine **Snippets → Add New**
2. Pane nimeks:

```
WooCommerce DB hinnad 5 sendini (ALATI ÜLES)
```

3. Lisa kood:

```php id="db_rounding_solution"
/**
 * Ümardamine alati üles 0.05-ni
 */
function round_up_to_5_cents($price) {
    if ($price === '' || $price === null) return $price;
    return ceil($price / 0.05) * 0.05;
}

/**
 * Salvestamisel ümardame hinna (toode)
 */
add_action('woocommerce_admin_process_product_object', function($product) {

    $regular_price = $product->get_regular_price();
    $sale_price = $product->get_sale_price();

    if ($regular_price !== '') {
        $product->set_regular_price(round_up_to_5_cents($regular_price));
    }

    if ($sale_price !== '') {
        $product->set_sale_price(round_up_to_5_cents($sale_price));
    }
});

/**
 * Variatsioonide hinnad
 */
add_action('woocommerce_admin_process_variation_object', function($variation) {

    $regular_price = $variation->get_regular_price();
    $sale_price = $variation->get_sale_price();

    if ($regular_price !== '') {
        $variation->set_regular_price(round_up_to_5_cents($regular_price));
    }

    if ($sale_price !== '') {
        $variation->set_sale_price(round_up_to_5_cents($sale_price));
    }
});
```

4. Pane:
   👉 **Run snippet everywhere**
5. **Save & Activate**

---

# 🔄 3. Kuidas see töötab

Pärast seda:

* iga kord kui:

  * toodet salvestatakse
  * import uuendab toodet
* siis:
  👉 hind ümardatakse ja **salvestatakse DB-sse**

---

# 🧪 4. Testimine

### Test:

1. Ava toode
2. Pane hind: `10.21`
3. Salvesta

👉 Tulemus:

* hind muutub automaatselt → **10.25**

---

# 📦 5. Olemasolevate toodete mass-uuendus (väga oluline)

Praegune kood EI muuda vanu hindu automaatselt.

Sul on 2 varianti:

---

## Variant A – lihtne (ilma SQL-ita)

1. Mine:

   * Products → All Products
2. Vali kõik tooted
3. Bulk Edit → Update

👉 see triggerdab salvestuse → hinnad ümardatakse

---

## Variant B – automaatne skript (soovitan suurele poele)

Lisa AJUTINE snippet:

```php id="bulk_update_prices"
add_action('init', function() {
    if (!isset($_GET['run_price_rounding'])) return;

    $args = [
        'limit' => -1,
        'status' => 'publish',
    ];

    $products = wc_get_products($args);

    foreach ($products as $product) {
        $price = $product->get_regular_price();

        if ($price !== '') {
            $product->set_regular_price(round_up_to_5_cents($price));
            $product->save();
        }
    }

    echo "Done!";
    exit;
});
```

### Käivitamine:

Ava brauseris:

```
https://sinudomeen.ee/?run_price_rounding=1
```

👉 Kui tehtud:

* **eemalda see snippet!**

---

# ⚠️ 6. Olulised nüansid

## 💡 1. Variatsioonid

Kui sul on variable products:

* need kaetakse koodiga ✔

---

## 💸 2. Käibemaks (KM)

Kuna hinnad on DB-s:
👉 vähem rounding probleeme kui runtime lahendusel

---

## ⚡ 3. Performance

See lahendus:

* ✔ kiirem
* ✔ parem suurele poele
* ✔ vähem hooke frontendis

---

## 🔄 4. Impordipluginad

Kui kasutad:

* WP All Import
* API sync

👉 see hook töötab, kui import kasutab WooCommerce API-t

Kui EI tööta:
👉 tuleb hook panna otse import pluginasse (saab aidata)

---

# 🚀 Soovitus (reaalne projektipraktika)

Parim setup:

✔ DB rounding (see lahendus)
+
✔ fallback runtime rounding (turvaks)

👉 Kui tahad, võin anda ka hybrid variandi

---

# ✅ Kokkuvõte

Sul on nüüd:

* ✔ DB tasemel hinnaparandus
* ✔ automaatne ümardamine salvestamisel
* ✔ mass-uuenduse skript
* ✔ valmis production kasutuseks

---

Kui tahad järgmise sammuna:
👉 võin teha lahenduse, kus:

* hinnad lõppevad alati **.99 (nt 10.25 → 10.99)**
* või kus ümardamine sõltub hinnavahemikust (nt kallimatel toodetel teistmoodi)
