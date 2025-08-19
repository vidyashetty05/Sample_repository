<?php
require_once 'Book.php';
require_once 'BookRepository.php';

$bookRepository = new BookRepository();

if (isset($_POST['add_book'])) {
    $book = new Book($_POST['title'], $_POST['author']);
    $bookRepository->addBook($book);
}

if (isset($_GET['delete_book_id']))  {
    $bookRepository->deleteBook($_GET['delete_book_id']);
}

$books = $bookRepository->getAllBooks();

?>

<!DOCTYPE html>
<html>
<head>
    <title>Book Repository</title>
</head>
<body>
    <h1>Book Repository</h1>
    <form action="" method="post">
        <input type="text" name="title" placeholder="Title">
        <input type="text" name="author" placeholder="Author">
        <button type="submit" name="add_book">Add Book</button>
    </form>
    <ul>
        <?php foreach ($books as $book) { ?>
            <li>
                <?php echo $book->getTitle(); ?> by <?php echo $book->getAuthor(); ?>
                <a href="?delete_book_id=<?php echo $book->getId(); ?>">Delete</a>
            </li>
        <?php } ?>
    </ul>
</body>
</html>

