## Question
 You're working on a secret team solving coded transmissions.

Your team is scrambling to decipher a recent message, worried it's a plot to break into a major European National Cake Vault. The message has been mostly deciphered, but all the words are backward! Your colleagues have handed off the last step to you.

Write a method reverseWords() that takes a message as an array of characters and reverses the order of the words in place. ↴

>Why an array of characters instead of a string?
>
>The goal of this question is to practice manipulating strings in place. Since we're modifying the message, we need a mutable ↴ type like an array, instead of Java's immutable strings.

For example:
```
  char[] message = { 'c', 'a', 'k', 'e', ' ',
                   'p', 'o', 'u', 'n', 'd', ' ',
                   's', 't', 'e', 'a', 'l' };

reverseWords(message);

System.out.println(message);
// prints: "steal pound cake"
```
When writing your method, assume the message contains only letters and spaces, and all words are separated by one space. 

## solution 1. convert into an array of word in String, and re-populate the cha[]
```java
    public static void reverseWords(char[] message) {

        // decode the message by reversing the words
        String[] words = new String(message).split(" ");
        int idx=0;
        for(int i=words.length-1; i>=0; --i){
            for(char c : words[i].toCharArray() ){
                message[idx++]=c;
            }
            
            if(i!=0){
                message[idx++]=' ';
            }
        }
    }
```

## Solution 2, the intresting find is, word swap can be done by all_character_swap+word_character_swap

```


Let's try manipulating a sample input by hand.

And remember what we did for our character-level reversal...

Look what happens when we do a character-level reversal:

  // input: the eagle has landed
{ 't', 'h', 'e', ' ', 'e', 'a', 'g', 'l', 'e', ' ',
  'h', 'a', 's', ' ', 'l', 'a', 'n', 'd', 'e', 'd' };

// character-reversed: dednal sah elgae eht
{ 'd', 'e', 'd', 'n', 'a', 'l', ' ', 's', 'a', 'h', ' ',
  'e', 'l', 'g', 'a', 'e', ' ', 'e', 'h', 't' };

Notice anything?

What if we put it up against the desired output:

  // input: the eagle has landed
{ 't', 'h', 'e', ' ', 'e', 'a', 'g', 'l', 'e', ' ',
  'h', 'a', 's', ' ', 'l', 'a', 'n', 'd', 'e', 'd' };

// character-reversed: dednal sah elgae eht
{ 'd', 'e', 'd', 'n', 'a', 'l', ' ', 's', 'a', 'h', ' ',
  'e', 'l', 'g', 'a', 'e', ' ', 'e', 'h', 't' };

// word-reversed (desired output): landed has eagle the
{ 'l', 'a', 'n', 'd', 'e', 'd', ' ', 'h', 'a', 's', ' ',
  'e', 'a', 'g', 'l', 'e', ' ', 't', 'h', 'e' };

The character reversal reverses the words! It's a great first step. From there, we just have to "unscramble" each word.

More precisely, we just have to re-reverse each word!

```

```java
    public static void reverseWords(char[] message) {
        // decode the message by reversing the words
        //step 1. reverse from start to end, by character;
        swap(message, 0, message.length-1);
        
        //step 2. for each word, swap it;
        for(int idx=0; idx<message.length; ){
            if(message[idx] == ' ' ){
                idx++;
                continue;
            }
            int tempS=idx;
            while(idx<message.length && message[idx] != ' '){
                idx++;
            }
            swap(message, tempS, idx-1);
        }

    }
    
    private static void swap(char[] message, int from, int to){
        while(from<to){
            char t = message[from];
            message[from]=message[to];
            message[to]=t;
            
            from++;
            to--;
        }
    }
```
