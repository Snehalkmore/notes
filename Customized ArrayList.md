```
class Book{
	String bookName;
	int bookId;
	
	public Book(String bookName, int bookId) {
		super();
		this.bookName = bookName;
		this.bookId = bookId;
	}	
}

class CustomizedBookList{
	public static void add(String[]bookName,int[]bookId) {
		ArrayList<Book> list = new ArrayList<>();
		for(int i=0;i<bookId.length;i++) {
			list.add(new Book(bookName[i],bookId[i]));
		}
		displayBooks(list);
	}

	private static void displayBooks(ArrayList<Book> list) {
		for(int i=0;i<list.size();i++) {
			System.out.println(list.get(i).bookId+" "+list.get(i).bookName);
		}
		
	}
}

public class CustomizedArrayListExample {

	public static void main(String[] args) {
		String[]bookNames = new String[] {"AB","CD","DE"};
		int[]bookIds = new int[] {1,2,3};
		
		CustomizedBookList.add(bookNames, bookIds);
	}

}

```
