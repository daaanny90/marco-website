<div class="page-container">
  <h1>Contacts</h1>

  <form class="contact-form" name="contact" method="POST" netlify>
    <p>
      <label>Your Name: <input type="text" name="name" /></label>
    </p>
    <p>
      <label>Your Email: <input type="email" name="email" /></label>
    </p>
    <p>
      <label>Message: <textarea name="message" /></label>
    </p>
    <p>
      <button type="submit">SEND</button>
    </p>
  </form>
  <input type="hidden" name="form-name" value="contact">
</div>

<style lang="scss">
  .contact-form {
    width: 100%;
    display: flex;
    flex-direction: column;
    align-items: center;

    p {
      width: 100%;
      text-align: center;

      label {
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
      }
      button {
        color: #ff3e00;
        background-color: transparent;
        outline: none;
        border: none;
        font-size: 2em;
        font-weight: lighter;
        cursor: pointer;

        &:hover {
          border: 1px solid #ff3e00;
          border-radius: 5px;
        }
      }
    }
  }
</style>
