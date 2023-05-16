
    <section>
      <h2>Contact Form</h2>
      <form id="contact-form">
        <label for="name">Name: </label>
          <input placeholder="Name" id="name" type="text" /><br>
        <label for="email">Email: </label>
          <input placeholder="Email" id="email" type="email" /><br>
        <textarea placeholder="Message"></textarea><br>
          <input type="submit" value="SEND">
      </form>
    </section>


        <script src="https://cdn.sendgrid.com/api/v3/js/sendgrid.min.js"></script>
      <script>
      const form = document.getElementById('contact-form');

      form.addEventListener('submit', function (event) {
        event.preventDefault();

        const name = document.getElementById('name').value;
        const email = document.getElementById('email').value;
        const message = document.getElementById('message').value;

        const data = {
          personalizations: [
            {
              to: [{ email: 'seguro7g@gmail.com' }],
              subject: 'Mensaje enviado desde el formulario de contacto'
            }
          ],
          from: { email: email, name: name },
          content: [
            {
              type: 'text/plain',
              value: message
            }
          ]
        };

        const request = SendGrid.post('/v3/mail/send', {
          headers: {
            Authorization: `Bearer ${SENDGRID_API_KEY}`
          },
          body: data,
          json: true
        });

        request.then(
          function (response) {
            console.log(response);
            alert('Correo electrónico enviado!');
          },
          function (error) {
            console.error(error);
            alert('Ha ocurrido un error al enviar el correo electrónico.');
          }
        );
      });
      </script>
