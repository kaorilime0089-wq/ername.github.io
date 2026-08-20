<!DOCTYPE html>
<html lang="ja">

<head>
    <meta charset="UTF-8">
    <meta name="viewport"
          content="width=device-width, initial-scale=1.0">

    <title>期間限定セール</title>

    <link rel="stylesheet" href="style.css">
</head>

<body>

<header>
    <h1>🔥 期間限定セール 🔥</h1>
    <p>今だけ5%OFF！</p>
</header>


<main>

    <section class="product">

        <img src="images/game.jpg"
             alt="商品画像">

        <h2>オリジナル商品</h2>

        <p class="normal-price">
            通常価格
            <span>5,980円</span>
        </p>

        <p class="sale-price">
            3,980円
        </p>

        <p class="discount">
            50% OFF
        </p>

        <p>
            セール期間：8月20日〜8月31日
        </p>

    </section>


    <section class="order">

        <h2>購入者情報</h2>

        <form id="orderForm">

            <label>
                お名前

                <input
                    type="text"
                    id="name"
                    required>
            </label>


            <label>
                メールアドレス

                <input
                    type="email"
                    id="email"
                    required>
            </label>


            <label>
                購入個数

                <input
                    type="number"
                    id="quantity"
                    value="1"
                    min="1"
                    required>
            </label>


            <h3>支払い方法</h3>

            <label class="payment">

                <input
                    type="radio"
                    name="paymentMethod"
                    value="bank"
                    checked>

                銀行振込

            </label>


            <button type="submit">
                注文する
            </button>

        </form>

    </section>


    <section
        id="result"
        class="result">

        <h2>注文完了</h2>

        <p>
            注文番号：
            <strong id="orderNumber"></strong>
        </p>

        <p>
            商品：
            <span id="resultProduct"></span>
        </p>

        <p>
            個数：
            <span id="resultQuantity"></span>
        </p>

        <p>
            お支払い金額：
            <strong>
                <span id="resultAmount"></span>円
            </strong>
        </p>

        <h3>銀行振込先</h3>

        <div class="bank">

            <p>
                銀行名：○○銀行
            </p>

            <p>
                支店名：○○支店
            </p>

            <p>
                口座種類：普通
            </p>

            <p>
                口座番号：1234567
            </p>

            <p>
                口座名義：カ）○○○○
            </p>

        </div>


        <p class="warning">
            振込手数料はお客様のご負担となります。
        </p>

        <p>
            入金確認後、商品を提供します。
        </p>

    </section>

</main>


<footer>
    <p>
        © 2026 私のショップ
    </p>
</footer>


<script>

const API_URL =
    "https://YOUR-API-DOMAIN.com";


document
    .getElementById("orderForm")
    .addEventListener(
        "submit",
        async function(event) {

            event.preventDefault();


            const name =
                document.getElementById(
                    "name"
                ).value;


            const email =
                document.getElementById(
                    "email"
                ).value;


            const quantity =
                Number(
                    document.getElementById(
                        "quantity"
                    ).value
                );


            try {

                const response =
                    await fetch(
                        API_URL +
                        "/api/orders",
                        {
                            method: "POST",

                            headers: {
                                "Content-Type":
                                    "application/json"
                            },

                            body:
                                JSON.stringify({

                                    productId:
                                        "game001",

                                    quantity:
                                        quantity,

                                    name:
                                        name,

                                    email:
                                        email,

                                    paymentMethod:
                                        "bank"

                                })
                        }
                    );


                const data =
                    await response.json();


                if (!response.ok) {

                    alert(
                        data.message ||
                        "注文に失敗しました。"
                    );

                    return;
                }


                document.getElementById(
                    "orderNumber"
                ).textContent =
                    data.orderNumber;


                document.getElementById(
                    "resultProduct"
                ).textContent =
                    data.productName;


                document.getElementById(
                    "resultQuantity"
                ).textContent =
                    data.quantity + "個";


                document.getElementById(
                    "resultAmount"
                ).textContent =
                    data.amount.toLocaleString();


                document.getElementById(
                    "result"
                ).style.display =
                    "block";


                document.getElementById(
                    "result"
                ).scrollIntoView({
                    behavior: "smooth"
                });

            }
            catch (error) {

                alert(
                    "サーバーに接続できませんでした。"
                );

                console.error(error);

            }

        }
    );

</script>

</body>
</html>
