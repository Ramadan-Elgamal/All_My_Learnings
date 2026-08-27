- Create an interface for a blog post with properties for title, content, author, and publication date.
```ts
interface Post{
	title: string;
	content: string;
	authorId: number;
	published_at: Date
}
```

- Extend that interface to create a `FeaturedBlogPost` interface with additional properties.
```ts
interface FeaturedBlogPost extends Post{
	thumbnail_url: string
	upvotes: number
}
```

-  Define an interface for a function that takes two strings and returns a boolean.
```ts
interface Function{
	(x: string, y: string) : boolean;
}

const isLonger: Function = (str1, str2) => {
	return str1.length > str2.lenght
}
```

- Create an interface with optional properties and readonly properties, then try to use it in a practical example.
```ts
interface KidsGame {
  readonly id: string;
  readonly sku: string;
  
  title: string;
  basePrice: number;
  inStock: boolean;
  
  minAge?: number;
  discountedPrice?: number;
}

const applyHolidayDiscount = (game: KidsGame, discountPercent: number): KidsGame => {

  const discountAmount = game.basePrice * (discountPercent / 100);

  return {
    ...game,
    discountedPrice: game.basePrice - discountAmount
  };
};

const memoryMatchGame: KidsGame = {
  id: "game_9876",
  sku: "MEM-MATCH-01",
  title: "Animal Memory Match",
  basePrice: 24.99,
  minAge: 4,
  inStock: true  
};

const saleItem = applyHolidayDiscount(memoryMatchGame, 20);

console.log(`Original Price: $${memoryMatchGame.basePrice}`);
console.log(`Sale Price: $${saleItem.discountedPrice}`);
```
