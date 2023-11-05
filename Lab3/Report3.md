# Lab Report 3
## Part 1
##### Reverse In Place bug
##### Initial code:
```java
static void reverseInPlace(int[] arr) {
    for(int i = 0; i < arr.length; i += 1) {
      arr[i] = arr[arr.length - i - 1];
    }
  }
```
##### Failure inducing input
```java
int[] input = {1,2,3};
ArrayExamples.reverseInPlace(input);
assertArrayEquals(new int[]{3,2,1}, input);
```
The expected output is `{3,2,1}` but the actual output is `{3,2,3}`.
##### Input that doesn't induce failure
```java
int[] input1 = {0,0};
    ArrayExamples.reverseInPlace(input1);
    assertArrayEquals(new int[]{0,0}, input1);
```
The input is `{0,0}` and the output is also `{0,0}`
##### Screenshot 1 (Failure inducing input):
![Image](FailureInducing.png)
##### Screenshot 2 (Non-Failure inducing input): 
![Image](NonFailure.png)

##### Before:
```java
static void reverseInPlace(int[] arr) {
    for(int i = 0; i < arr.length; i += 1) {
      arr[i] = arr[arr.length - i - 1];
    }
  }
```
##### After:
```java
static void reverseInPlace(int[] arr) {
    int temp ;
    for(int i = 0; i < arr.length / 2; i++) {
      temp = arr[i];
      arr[i] = arr[arr.length - i - 1];
      arr[arr.length - i - 1] = temp;
    }
  }
```
###### Explanation:
I basically created a temporary variable `temp` to keep track of the current number. Then I was able to change the number at the current index with the number at `arr.length-i-1`. And then I was able to change the number at `arr.length-i-1` to the first number because now I actually have that number stored in a temporary variable. <br>
Before creating the temporary variable, the function was just passing through the array and replacinf the number at the current index `i` with the number at index `arr.length-i-1`. This was producing the incorrect output because it was not keeping track of the number at the current index and swapping it with `arr.lentgh-i-1`.

## Part 2

#### Number 1 - counting the amount of times a specific word occurs:
##### Example 1:
```java
$grep -ro "god" ./technical | wc -l

53
```
##### Example 2:
```java
$ grep -ro "statement" ./technical/biomed | wc -l

74
```
##### Explanation:
- The `-r` option in `grep` enables a recursive search within directories. When combined with the `-r` flag, `grep` searches for the specified parameter, in this case "god", in all files within the given directory, in this case `technical` and `technical/biomed`, and its subdirectories.

- The `-o` option in `grep` tells `grep` to output only the matched parts of the lines rather than entire lines. So if we run `grep -ro "god" ./technical`, it will return the files that include god and the word god itself. 

- `wc -l` command stands for "word count". When used with the `-l`, it counts the number of lines. By piping the output of grep to wc `-l`, it calculates the total number of lines that grep finds in the files. Since `-o` in grep ensures that each match is on a separate line, `wc -l` effectively counts the total number of occurrences of the word or pattern. 

- Therefore, combining `grep -ro "god" ./technical | wc -l` displays the amount of times that the word "god" appears withing the files inside the `techncial` directory. We can change the word that we are looking for as well the specific directory that we look into, making this very useful if looking for a specific statement, word, or sentence.
#### Number 2 - finding the line that the specific word is placed at:
##### Example 1: 
```java
$ grep -nr "imagine" ./technical/biomed

./technical/biomed/1471-213X-1-13.txt:383:          dlA dx2 mutant embryos. We imagined
./technical/biomed/1471-2148-3-3.txt:138:        away from this genotype by adding mutations, imagine that
./technical/biomed/1471-2156-3-4.txt:763:          previously imagined.
./technical/biomed/1471-2164-3-19.txt:273:        imagine two szenarios making ROC analysis inappropriate for
./technical/biomed/1471-2202-3-5.txt:158:          perspective: If we imagine that
./technical/biomed/1471-2288-2-11.txt:12:          change the age of death. As an analogy, imagine waiting
./technical/biomed/1471-2288-3-9.txt:69:        - in what they imagined to be a flawless mechanistic
./technical/biomed/1471-2431-2-11.txt:15:        classroom students sometimes use self-hypnosis to imagine
./technical/biomed/1471-2431-2-11.txt:111:        control. Typically, children chose to imagine a favorite
./technical/biomed/1471-2431-2-11.txt:114:        symptom. For example, some patients learned to imagine the
./technical/biomed/1471-2431-2-11.txt:116:        to imagine changing the appearance to a normal one.
./technical/biomed/1471-2431-2-11.txt:128:        in a few minutes, by suggesting that the patient imagine
./technical/biomed/1471-2458-3-20.txt:354:        accurately imagined. Nonetheless, it is worth noting that
./technical/biomed/1472-6750-2-21.txt:329:          such as luciferase. It is also possible to imagine that
./technical/biomed/1472-684X-2-1.txt:272:        system, it is easy to imagine how a resident's reluctance
./technical/biomed/1476-4598-2-28.txt:579:        101 ] , as one can imagine that the cooperative action of
./technical/biomed/1477-7827-1-13.txt:508:          one might imagine, e.g. just placental aging. Table
./technical/biomed/gb-2001-2-4-research0010.txt:785:        imagined.
./technical/biomed/gb-2001-2-4-research0012.txt:328:          imagined) so that diagrams can be easily drawn by hand or
```
##### Example 2:
```java
grep -nr "god" ./technical > godIntechnical.txt
```
##### Output: 
![Image](godTech.png)

###### Explanation: 
- The `-n` displays the line number with the matched line. When used, `grep` will print the line number before each line containing the matched pattern/paramtere, in this case "god" and "imagine".
- In the first example, we are looking for the word "imagine" inside the `biomed` folder. The terminal directly returns every occurrence of imagine with the specific file and line.
- In the second case, we looked for the word "god" inside the entire `technical` directory and then stored all of the occurrences inside a `.txt` file named `godIntechnical`. This is practical when there are a lot of occurrences of a certain pattern because insetad of having 1,000 lines of code on the terminal, we store them inside a `.txt` file and can use that in other cases.
#### Number 3 - before-context and after-context:
##### Example 1:
```java
$grep -m 1 -B 2 -A 2 "emergency" ./technical/911report/chapter-1.txt

    The hijackers quickly gained control and sprayed Mace, pepper spray, or some other irritant in the first-class cabin, in order to force the passengers and flight attendants toward the rear of the plane. They claimed they had a bomb.

    About five minutes after the hijacking began, Betty Ong contacted the American Airlines Southeastern Reservations Office in Cary, North Carolina, via an AT&T airphone to report an emergency aboard the flight. This was the first of several occasions on 9/11 when flight attendants took action outside the scope of their training, which emphasized that in a hijacking, they were to communicate with the cockpit crew. The emergency call lasted approximately 25 minutes, as Ong calmly and professionally relayed information about events taking place aboard the airplane to authorities on the ground.     

    At 8:19, Ong reported:"The cockpit is not answering, somebody's stabbed in business class-and I think there's Mace-that we can't breathe-I don't know, I think we're getting hijacked." She then told of the stabbings of the two flight attendants.
```
##### Example 2: 
```java
$grep -r -m 1 -B 1 -A 1 "God" ./technical/biomed

./technical/biomed/1471-2091-2-13.txt-        The dispersion of the intein as a selfish genetic
./technical/biomed/1471-2091-2-13.txt:        element is consistent with the work of Goddard and Burt [
./technical/biomed/1471-2091-2-13.txt-        38 ] on the persistence of an intron with homing
--
./technical/biomed/1471-2172-2-10.txt-          +individuals (Hispanic) under the direction of Dr. Harold
./technical/biomed/1471-2172-2-10.txt:          I. Laroche and Dr. E. Godreau, Center for Diagnosis and
./technical/biomed/1471-2172-2-10.txt-          Treatment, Ponce. The aged population, recruited from the
--
./technical/biomed/1471-2210-1-3.txt-          culture medium. Separation of islets was carried out
./technical/biomed/1471-2210-1-3.txt:          using dispase (1000 U/ml, Godo Shusei, Japan) as
./technical/biomed/1471-2210-1-3.txt-          previously described [ 35 ] . Separated cells were again
--
./technical/biomed/1472-6882-1-7.txt-          Hallelujah Acres, Inc. (
./technical/biomed/1472-6882-1-7.txt:          God's Way to Ultimate Health, Recipes
./technical/biomed/1472-6882-1-7.txt-          for Life...from God's Garden, 21 Days to health the
--
./technical/biomed/1477-7827-1-17.txt-          bovine IFNγ (200 IU/ml; generous gift from Dr. Dale
./technical/biomed/1477-7827-1-17.txt:          Godson, Veterinary Infectious Disease Organization,
./technical/biomed/1477-7827-1-17.txt-          University of Saskatchewan, Saskatoon, Saskatchewan,
--
./technical/biomed/gb-2002-3-10-research0055.txt-          'tryptophanyl-tRNA synthetase', 'Sky' = 'TYRO3 protein
./technical/biomed/gb-2002-3-10-research0055.txt:          tyrosine kinase', 'God' = 'Godzilla'). Short acronyms are
./technical/biomed/gb-2002-3-10-research0055.txt-          especially problematic (for example, 'CT', the
```
