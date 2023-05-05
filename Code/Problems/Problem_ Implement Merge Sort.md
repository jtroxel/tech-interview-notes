```
void merge(int[] sequence, int left, int middle, int right) {
  int[] result = new int[right - left];
  int i, j;
  int k = 0;

  System.out.print("merging.. " + left + ".." + middle + ".." + (right-1) + "\t");

  // Progress through both sides, 2 pointers, inserting the minimum val
  for (i = left, j = middle; i < middle && j < right; ) {
    if (sequence[i] < sequence[j]) {
      result[k++] = sequence[i];
      i++;
    }
    else {
      result[k++] = sequence[j];
      j++;
    }
  }

  // Finish off ends if unbalanced
  while (i < middle) {
    result[k++] = sequence[i];
    i++;
  }

  while (j < right) {
    result[k++] = sequence[j];
    j++;
  }

  // put results back into original
  for (i = left; i < right; i++) {
    sequence[i] = result[i - left];
    System.out.print(sequence[i] + " ");
  }
  System.out.println();
}

void split(int[] sequence, int left, int right) {
  if (left + 1 == right) {

   System.out.println("\tsplat " + left + ".." + (right-1) + "\t = " + sequence[left]);

    return;
  }
  int middle = (left + right) / 2;
  System.out.println("splitting " + left + ".." + middle + ".." + (right-1));
  split(sequence, left, middle);
  split(sequence, middle, right);
  merge(sequence, left, middle, right);
}

int[] solution(int[] sequence) {
  split(sequence, 0, sequence.length);

  return sequence;
}
```