---
layout: post
title:  Allocation
categories: v8
tags: [v8,cpp,memory]
---

## Allocation in V8
V8 allocate C free store using malloc and free.
```cpp
void* Malloced::New(size_t size) {
  ASSERT(NativeAllocationChecker::allocation_allowed());
  void* result = malloc(size);
  if (result == NULL) V8::FatalProcessOutOfMemory("Malloced operator new");
  return result;
}


void Malloced::Delete(void* p) {
  free(p);
}
```
Besides of that, V8 defined a `PreallocatedStorage` (double linked list) to manage allocated memorry.
Link chunks ![link-chunks](/assets/images/PreallocatedStorage-LinkTo.png){:class="ioda"}

Unlink ![unlink-chunk](/assets/images/PreallocatedStorage-Unlink.png){:class="ioda"}

When we need to allocate some memorry, first V8 will find available memorry chunk in `free_list_` that fit before call `Malloced::New()` to allocate new memorry. And when V8 done using a memorry chunk, it does not `free` instantly. Instead, V8 just removes the chunk from `in_use_list_` and move it to `free_list_`.
![find-fit-memorry-chunk](/assets/images/PreallocatedStorage-New-1.png){:class="ioda"}
 So when we need memorry to store something else, we just override data on allocated memory, it save us one free operation.
 ![add-free-chunk-to-in-used](/assets/images/PreallocatedStorage-New-2.png){:class="ioda"}
There is nothing much to be done in allocation since it just a wrapper to `malloc` and `free` memorry. But this is the heart of everything. In next posts, we will see how `PreallocatedStorage` is used by V8 in specific scenarios.
