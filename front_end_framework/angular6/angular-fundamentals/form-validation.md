Form Validation
---

## Reactive form validation

In a reactive form, the source of truth is the component class. Instead of adding validators through attributes in the template, you add validator functions directly to the form control model in the component class.

There are two types of validator functions: sync validators and async validators.

- Sync validators: functions that take a control instance and immediately return either a set of validation errors or null. You can pass these in as the second argument when you instantiate a `FormControl`.

- Async validators: functions that take a control instance and return a Promise or Observable that later emits a set of validation errors or null. You can pass these in as the third argument when you instantiate a `FormControl`.


## Built-in validators

`Validators` class provides a set of built-in validators that can be used by form controls.

```ts
class Validators {
  static min(min: number): ValidatorFn
  static max(max: number): ValidatorFn
  static required(control: AbstractControl): ValidationErrors | null
  static requiredTrue(control: AbstractControl): ValidationErrors | null
  static email(control: AbstractControl): ValidationErrors | null
  static minLength(minLength: number): ValidatorFn
  static maxLength(maxLength: number): ValidatorFn
  static pattern(pattern: string | RegExp): ValidatorFn
  static nullValidator(control: AbstractControl): ValidationErrors | null
  static compose(validators: (ValidatorFn | null | undefined)[] | null): ValidatorFn | null
  static composeAsync(validators: (AsyncValidatorFn | null)[]): AsyncValidatorFn | null
}

```


```ts
this.heroForm = new FormGroup({
    'name': new FormControl(this.hero.name, [
      Validators.required,
      Validators.minLength(4),
      forbiddenNameValidator(/bob/i) // <-- Here's how you pass in the custom validator.
    ]),
    'alterEgo': new FormControl(this.hero.alterEgo),
    'power': new FormControl(this.hero.power, Validators.required)
  });

  get name() { return this.heroForm.get('name'); }

  get power() { return this.heroForm.get('power'); }
```

- The name control sets up two built-in validators—Validators.required and Validators.minLength(4)—and one custom validator, forbiddenNameValidator. For more details see the Custom validators section in this guide.

- As these validators are all sync validators, you pass them in as the second argument.

- Support multiple validators by passing the functions in as an array.

- This example adds a few getter methods. In a reactive form, you can always access any form control through the get method on its parent group, but sometimes it's useful to define getters as shorthands for the template.





























---
