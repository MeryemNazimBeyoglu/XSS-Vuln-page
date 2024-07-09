<?php
$servername = "localhost";
$username = "vuluser";
$password = "vulpass";
$dbname = "yorum_sayfasi_db";

// MySQL bağlantısı oluştur
$conn = new mysqli($servername, $username, $password, $dbname);

// Bağlantıyı kontrol et
if ($conn->connect_error) {
    die("Bağlantı hatası: " . $conn->connect_error);
}

// Yeni yorum eklemek için form gönderildi mi kontrol et
if ($_SERVER["REQUEST_METHOD"] == "POST") {
    $kullanici_adi = $conn->real_escape_string($_POST['username']);
    $yorum = $conn->real_escape_string($_POST['comment']);

    // SQL sorgusu ile veritabanına ekle
    $sql = "INSERT INTO yorumlar (kullanici_adi, yorum) VALUES ('$kullanici_adi', '$yorum')";

    if ($conn->query($sql) === TRUE) {
        // Yorum eklendikten sonra index.php'ye yönlendir
        header('Location: index.php');
        exit();
    } else {
        echo "Hata: " . $sql . "<br>" . $conn->error;
    }
}

// Yorumları veritabanından çek
$sql = "SELECT kullanici_adi, yorum, tarih FROM yorumlar ORDER BY tarih DESC";
$result = $conn->query($sql);

$conn->close();
?>

<!DOCTYPE html>
<html lang="tr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Yorum Sayfası</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #f4f4f9;
            margin: 0;
            padding: 0;
            display: flex;
            flex-direction: column;
            align-items: center;
        }
        h1 {
            color: #333;
            margin-top: 50px;
        }
        form {
            background: #fff;
            padding: 20px;
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
            border-radius: 8px;
            margin-top: 20px;
            width: 300px;
            display: flex;
            flex-direction: column;
        }
        label {
            margin-bottom: 10px;
            color: #555;
        }
        input[type="text"], textarea {
            padding: 10px;
            margin-bottom: 15px;
            border: 1px solid #ddd;
            border-radius: 4px;
            width: 100%;
        }
        input[type="submit"] {
            padding: 10px;
            border: none;
            background: #28a745;
            color: white;
            border-radius: 4px;
            cursor: pointer;
            font-size: 16px;
        }
        input[type="submit"]:hover {
            background: #218838;
        }
        #comments {
            width: 80%;
            margin-top: 30px;
        }
        #comments p {
            background: #fff;
            padding: 10px;
            border: 1px solid #ddd;
            border-radius: 4px;
            margin-bottom: 10px;
        }
        #comments strong {
            color: #333;
        }
    </style>
</head>
<body>
    <h1>Yorum Yap</h1>
    <form method="POST" action="<?php echo htmlspecialchars($_SERVER["PHP_SELF"]); ?>">
        <label for="username">Kullanıcı Adı:</label>
        <input type="text" id="username" name="username" required>
        <label for="comment">Yorum:</label>
        <textarea id="comment" name="comment" rows="4" required></textarea>
        <input type="submit" value="Gönder">
    </form>
    <h2>Yorumlar</h2>
    <div id="comments">
        <?php
        // Yorumları göster
        if ($result && $result->num_rows > 0) {
            while($row = $result->fetch_assoc()) {
                echo "<p><strong>" . $row["kullanici_adi"] . "</strong>: " . $row["yorum"] . " <br><small>" . $row["tarih"] . "</small></p>";
            }
        } else {
            echo "<p>Henüz yorum yapılmamış.</p>";
        }
        ?>
    </div>
</body>
</html>
