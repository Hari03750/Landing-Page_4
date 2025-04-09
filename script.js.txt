document.addEventListener('DOMContentLoaded', function () {
  const form = document.querySelector('form');

  form.addEventListener('submit', function (event) {
    // Prevent the form from submitting
    event.preventDefault();

    // Clear previous error messages
    clearErrors();

    // Perform validation checks
    let isValid = true;

    // Validate Full Name
    const nameInput = document.getElementById('name');
    if (nameInput.value.trim() === '') {
      displayError(nameInput, 'Full Name is required.');
      isValid = false;
    }

    // Validate Email
    const emailInput = document.getElementById('email');
    if (emailInput.value.trim() === '') {
      displayError(emailInput, 'Email is required.');
      isValid = false;
    } else if (!isValidEmail(emailInput.value)) {
      displayError(emailInput, 'Please enter a valid email address.');
      isValid = false;
    }

    // Validate Phone Number
    const phoneInput = document.getElementById('phone');
    if (phoneInput.value.trim() === '') {
      displayError(phoneInput, 'Phone Number is required.');
      isValid = false;
    } else if (!isValidPhone(phoneInput.value)) {
      displayError(phoneInput, 'Please enter a valid 10-digit phone number.');
      isValid = false;
    }

    // Validate Program Selection
    const programSelect = document.getElementById('program');
    if (programSelect.value === '') {
      displayError(programSelect, 'Please select a program.');
      isValid = false;
    }

    // If all validations pass, submit the form
    if (isValid) {
      form.submit();
    }
  });

  // Function to display error messages
  function displayError(input, message) {
    const errorDiv = document.createElement('div');
    errorDiv.className = 'error-message';
    errorDiv.innerText = message;
    input.parentElement.appendChild(errorDiv);
    input.classList.add('input-error');
  }

  // Function to clear all error messages
  function clearErrors() {
    const errorMessages = document.querySelectorAll('.error-message');
    errorMessages.forEach(function (error) {
      error.remove();
    });

    const errorInputs = document.querySelectorAll('.input-error');
    errorInputs.forEach(function (input) {
      input.classList.remove('input-error');
    });
  }

  // Function to validate email format
  function isValidEmail(email) {
    const emailRegex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
    return emailRegex.test(email);
  }

  // Function to validate phone number format
  function isValidPhone(phone) {
    const phoneRegex = /^\d{10}$/;
    return phoneRegex.test(phone);
  }
});
