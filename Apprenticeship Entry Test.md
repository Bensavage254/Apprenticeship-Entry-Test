SECTION 1: Logic & Problem Solving (10 marks)
Question 1:
 Write a function that returns the second-largest number in a given list of integers.
 (Provide your code and a short explanation of your approach.)

I first use a Set to remove duplicate numbers, ensuring uniqueness. Then, I sort the array in descending order using a custom comparator (a, b) => b - a. Finally, I return the element at index 1, which represents the second-largest unique number. If the list has fewer than two unique values, the function returns null.

function secondLargest(numbers) {
  // Remove duplicates using Set
  const uniqueNumbers = [...new Set(numbers)];

  // Check if there are at least two unique numbers
  if (uniqueNumbers.length < 2) {
    return null; // No second largest number
  }

  // Sort in descending order
  uniqueNumbers.sort((a, b) => b - a);

  // Return the second element
  return uniqueNumbers[1];
}

// Example usage
console.log(secondLargest([10, 20, 4, 45, 99])); // Output: 45






Question 2:
 Explain how you would optimize a page that loads too slowly. Mention at least three causes and how you’d fix each.

1.Large or unoptimized images: Oversized images increase load time. I would compress them using tools like TinyPNG, convert them to WebP format, and implement lazy loading so images load only when visible on the screen.
2.Lack of caching: Without caching, browsers repeatedly request the same resources. I’d enable browser caching and server-side caching (like Redis or CDN edge caching) to reduce repeated downloads and server load.
3.Too many or heavy JavaScript/CSS files: Multiple or bulky files block rendering. I would minify and bundle scripts and styles, remove unused code, and apply async or defer attributes on non-critical scripts to speed up initial page rendering




SECTION 2: Web/Software Development (15 marks)
Question 3 (Front-end):
 You are creating a simple profile page that fetches user data from an API (https://jsonplaceholder.typicode.com/users/1).
 Explain or show code for:
Fetching and displaying the user’s name and email.


Handling the loading and error states.


(You may use plain JS, React, or any stack you’re comfortable with.)


I used the useEffect hook to fetch data from the API when the component mounts. While the data is being fetched, a loading message appears. If the request fails, an error message is displayed. Once successful, the user’s name and email are rendered. This approach ensures good user experience by clearly showing each state loading, error, or data display.

import React, { useEffect, useState } from "react";

function UserProfile() {
  const [user, setUser] = useState(null);       // Store user data
  const [loading, setLoading] = useState(true); // Loading state
  const [error, setError] = useState(null);     // Error state

  useEffect(() => {
    fetch("https://jsonplaceholder.typicode.com/users/1")
      .then((response) => {
        if (!response.ok) {
          throw new Error("Network response was not ok");
        }
        return response.json();
      })
      .then((data) => {
        setUser(data);
        setLoading(false);
      })
      .catch((err) => {
        setError(err.message);
        setLoading(false);
      });
  }, []);

  if (loading) return <p>Loading user data...</p>;
  if (error) return <p>Error: {error}</p>;

  return (
    <div style={{ fontFamily: "Arial", margin: "20px" }}>
      <h2>User Profile</h2>
      <p><strong>Name:</strong> {user.name}</p>
      <p><strong>Email:</strong> {user.email}</p>
    </div>
  );
}

export default UserProfile;






Question 4 (Back-end / Logic):
 A small store wants to calculate total sales from this dataset:
[
  {"item": "Pen", "price": 20, "quantity": 3},
  {"item": "Book", "price": 200, "quantity": 2},
  {"item": "Bag", "price": 800, "quantity": 1}
]

Write a short function to calculate the total revenue.

I used the reduce() method to iterate through the list of items and accumulate the sum of price × quantity for each product. The function starts from 0 and keeps adding each item’s total cost. For the given dataset, the total revenue is (20×3) + (200×2) + (800×1) = 1260.

function calculateTotalSales(sales) {
  // Use reduce to sum up (price * quantity) for each item
  return sales.reduce((total, item) => total + item.price * item.quantity, 0);
}

// Example dataset
const data = [
  { item: "Pen", price: 20, quantity: 3 },
  { item: "Book", price: 200, quantity: 2 },
  { item: "Bag", price: 800, quantity: 1 }
];

console.log("Total Revenue:", calculateTotalSales(data)); // Output: 1260




SECTION 3: Debugging & Reasoning (10 marks)
Question 5:
 You’ve been given this code snippet:
numbers = [1, 2, 3, 4, 5]
for i in range(len(numbers)):
    if i % 2 == 0:
        numbers.remove(i)
print(numbers)

What’s wrong with the code?

The problem is that numbers.remove(i) removes the value equal to i, not the element at index i. Also, removing items from a list while iterating over it changes its length and shifts the indices, causing elements to be skipped or unexpected behavior.


What will it output?

When this runs:

i = 0 → removes 0 (not found, so no effect)

i = 1 → skip

i = 2 → removes 2

i = 3 → skip

i = 4 → removes 4

Final output:[1, 3, 5]



How would you fix it to remove even numbers correctly?

You should remove numbers based on their value, not index, and avoid modifying the list while iterating over it. A clean fix is:

numbers = [1, 2, 3, 4, 5]
numbers = [num for num in numbers if num % 2 != 0]
print(numbers)  # Output: [1, 3, 5]

This uses a list comprehension to create a new list containing only odd numbers, avoiding the issues that come with removing elements during iteration.




SECTION 4: Version Control & Collaboration (5 marks)
Question 6:
 Explain how you would use Git to collaborate on a team project with other developers.
 Mention at least:
One common Git command you use often.


One problem you’ve faced while using Git and how you solved it.

When collaborating on a team project using Git, I usually start by cloning the repository with git clone to get a local copy of the codebase. Each developer works on a separate branch using git checkout -b branch-name, which helps isolate features and prevent conflicts. One common Git command I use often is git pull, which keeps my local branch updated with the latest changes from the remote repository before pushing my own updates. A common problem I’ve faced is merge conflicts when two developers edit the same file section. I solved this by using Git’s conflict markers to manually compare both versions, keeping the correct changes, and then committing the resolved file with git add and git commit. This approach ensures smooth teamwork, version control, and code integration across the project.

