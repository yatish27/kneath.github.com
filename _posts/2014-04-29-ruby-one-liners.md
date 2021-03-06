---
layout: post
title: Ruby one liners for simple problems
summary: Ruby is one of the most flexible, purely object-oriented language. As a code craftsman, one falls for its elegance and beauty.
---

Ruby is one of the most flexible, purely object-oriented language. As a code craftsman, one falls for its elegance and beauty. Recently, I was conducting a training program for beginners in Ruby programming.

We decide to solve the following problems

* Prime number detection
* Factorial calculation
* Fibonacci Series
* Palindrome detection
* Pascal triangle calculation
* Sentence reversal.

We came up with ruby one liners to try to solve these problems

{% highlight ruby %}
def prime?(num)
  (2..Math.sqrt(num)).each { |int| return false if num % int == 0 }
  true
end

# Returns factorial of the *num*
def factorial(num)
  (1..num).reduce(1) { |fact, item| fact * item }
end

# Returns an array of fibonnaci series
def fibonnaci(num)
  (1..num - 2).reduce([0, 1]) { |fact| fact << fact[-1] + fact[-2] }
end

# Returns true if the binary of *num* is a palindrome
def palindrome?(num)
  num.to_s(2) == num.to_s(2).reverse
end

# Return array of arrays being a pascal triangle till *num* no of rows
def pascal(num)
  pascal = [[1], [1, 1]]
  (num - 2).times do
    ret = []
    (pascal.last.length - 1).times do |i|
      ret << pascal.last[i] + pascal.last[i + 1]
    end
    pascal.push [1, ret, 1].flatten
  end
  pascal
end

# Reverse the order of words in a sentence
def reverse_sentence(str)
  str.split(" ").reverse.join(" ")
end
{% endhighlight %}

Testing is an intergral part of programming. From a full fledged Rails application to a simple script, accompanying specs helps in increasing the confidence of your code.

I love rspec. It is a simple, behaviour driven testing framework.

{% highlight ruby %}
require 'rspec'
require './test.rb'

describe 'prime?' do
  context 'when the number is prime' do
    it { expect(prime?(13)).to be true }
  end

  context 'when the number is not prime' do
    it { expect(prime?(21)).to be false }
  end
end

describe 'factorial' do
  context 'when number is positive' do
    it { expect(factorial(5)).to eq(120) }
  end

  context 'when number is zero' do
    it { expect(factorial(0)).to eq(1) }
  end
end

describe 'fibonnaci' do
  context 'when a number is given' do
    it { expect(fibonnaci(5)).to eql([0, 1, 1, 2, 3]) }
  end
end

describe 'palindrome?' do
  context 'when the given number is a palindrome in binary' do
    it { expect(palindrome?(7)).to be true }
  end

  context 'when the given number is not a palindrome in binary' do
    it { expect(palindrome?(6)).to be false }
  end
end

describe 'pascal' do
  it 'should return an array of arrays of pascal triangle' do
    expect(pascal(3)).to eql([[1], [1, 1], [1, 2, 1]])
  end
end

describe 'reverse_sentence' do
  let(:sentence) { 'My name is Yatish' }
  let(:reverse)  { 'Yatish is name My' }
  it 'should return the reverse of the sentence' do
    expect(reverse_sentence(sentence)).to eq(reverse)
  end
end
{% endhighlight %}

Ruby programming language is clean and simple. This makes it popular among the novice programmers.
