---
layout: post
title:  "Chrome Autofill Bug Fix"
date:   2021-08-26 15:22:00 -0000
categories: JS, HTML
---


# Issue:<br />
I was running into an issue with Chrome defaulting the autofill in front of the google places autocomplete feature on an text input element for users to enter an address. I wanted it to function like a normal address autocomplete using the google places API but what it was doing was overlaying the in browser saved addressed in front of the actual autocomplete that I wanted. 

I tried adding all of the attributes like autocomplete="new-password", autocomplete="false" and autocomplete="off" to the input element with no success and decided to just start changing the input and labels to see what chrome was looking for. For a visual representation of what I am talking about, see below.

# What is was doing
![useful image]({{ site.url }}/assets/annoying_issue.png)

# What I wanted it to do
![useful image]({{ site.url }}/assets/annoying_issue_fixed.png)

# How To Fix It
It looks like chrome is looking for two things in it's autofill feature. It is checking the label for the word "address" and also checking the placeholder for the word "address". The workaround I found was to not use a label but create my own class called fake-label with the bootstrap css and then remove the placeholder completely since ng-google-places-autcomplete provides a placholder by default. See below for the differences:<br />

**Code that gets blocked by auto-fill**
```html
<div class="form-group">
    <label for="inputRecipientAddress">Recipient Address</label>
    <input type="text" autocomplete="new-password" formControlName="recipientAddress" class="form-control" id="inputRecipientAddress"  ngx-google-places-autocomplete  (onAddressChange)="addressChange($event)" placeholder="Enter Address">
    <div *ngIf="submitted && f.recipientAddress.errors" class="invalid-feedback">
        <div *ngIf="f.recipientAddress.errors.required">Address is required</div>
    </div>
</div>
```

**Code that removes blocking autofill:**
```html
<div class="form-group">
    <div class="fake-label"> for="inputRecipientAddress">Recipient Address</div>
    <input type="text" autocomplete="new-password" formControlName="recipientAddress" class="form-control" id="inputRecipientAddress"  ngx-google-places-autocomplete  (onAddressChange)="addressChange($event)">
    <div *ngIf="submitted && f.recipientAddress.errors" class="invalid-feedback">
        <div *ngIf="f.recipientAddress.errors.required">Address is required</div>
    </div>
</div>
```

This fixes the issue and allows the autocomplete feature that we want to be coming up front to work. Once you remove the placeholder from the input and create a class called fake-label that mimics the label for your specific css, it wont throw the autofill in front of the autocomplete. Hopefully this saves at least one person some time.

