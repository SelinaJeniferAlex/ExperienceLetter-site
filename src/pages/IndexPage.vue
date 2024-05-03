<template>
  <q-page class="flex flex-center">
    <div class="q-pa-md mobwidth"  v-if="hideForm">
      <q-form @submit="addItems" class="q-gutter-md">
        <div class="row justify-around">
          <div class="col-10 col-sm-5">
            <q-input filled v-model="name" label="Enter name *" lazy-rules
              :rules="[(val) => (val && val.length > 0) || 'please enter name']" />
          </div>
          <div class="col-10 col-sm-5">
            <q-input filled v-model="empcode" type="text" label="Enter Employee Code*" lazy-rules
              :rules="[(val) => (val && val.length > 0) || 'Please enter employee code']" />
          </div>
        </div>
        <div class="row justify-around">
          <div class="col-10 col-sm-5">
            <q-input filled v-model="email" type="email" label="Enter email *" lazy-rules
              :rules="[(val) => (val && val.length > 0) || 'Please enter email']" />
          </div>
          <div class="col-10 col-sm-5">
            <q-input filled v-model="designation" type="text" label="Enter Designation *" lazy-rules
              :rules="[(val) => (val && val.length > 0) || 'Please enter designation']" />
          </div>
        </div>
        <div class="row justify-around">
          <div class="col-10 col-sm-5">
            <q-input filled v-model="location" type="text" label="Enter Location*" lazy-rules
              :rules="[(val) => (val && val.length > 0) || 'Please enter location']" />
          </div>
          <div class="col-10 col-sm-5">
            <q-input filled v-model="joindate" type="date" label="Date of Joining *" lazy-rules
              :rules="[(val) => (val && val.length > 0) || 'Please enter date of joining']" />
          </div>
        </div>
        <div class="row justify-around">
          <div class="col-10 col-sm-5">
            <q-input filled v-model="resignationdate" type="date" label="Date of Resignation *" lazy-rules
              :rules="[(val) => (val && val.length > 0) || 'Please enter date of resignation']" />
          </div>
          <div class="col-10 col-sm-5">
            <q-input filled v-model="enddate" type="date" label="Date of Leaving *" lazy-rules
              :rules="[(val) => (val && val.length > 0) || 'Please enter date of leaving']" />
          </div>
        </div> <br>
        <div class="flex flex-center row">
          <q-btn class="col-11 q-pa-md" label="Generate Letter" type="submit" color="secondary" />
        </div>
      </q-form>
    </div>
    <br>
    <div style="max-width: 800px; margin: 20px" v-if="showLetter">
      <div id="ServiceLetter">
        <div style="padding: 20px;">
          <div class="row justify-between">
            <div class="col-4 column items-center justify-center">
              <h4><b>Entity Name</b></h4>
            </div>
            <div class="col-4 column items-center justify-center">
              <div>
                <div>
                  XXX Complex <br>
                  YYYYY YYYY Street <br>
                  TamilNadu, India
                </div>
              </div>
            </div>
          </div> <br>
          <div class="row">
            <div>
              <div>{{ enddate }}</div> <br>
              <div>Name: {{ name }}</div>
              <div>Employee ID: {{ empcode }}</div>
              <div>Location: {{ location }}</div>
            </div>
          </div>
          <div class="flex flex-center q-ma-sm">
            <div style="text-align: center;">
              <u>
                <p>RELIEVING CUM SERVICE CERTIFICATE</p>
              </u>
            </div>
          </div>
          <div class="row">
            <div class="col">
              <p>
                With reference to your resignation dated <b>{{ resignationdate }}</b>, we hereby accept your resignation from the services <br>
                of the company. Please note that you have been relieved from the services of the company effective <br>
                close of business hours on <b>{{ enddate }}</b>.
              </p>
            </div>
          </div>
          <div class="row">
            <div class="col">
              <div>Your service record with the Company is as follows:</div> <br>
              <div>Date of Joining : {{ joindate }}</div>
              <div>Date of Leaving : {{ enddate }}</div>
              <div>Current Designation : {{ designation }}</div>
            </div>
          </div> <br>
          <div class="row">
            <div class="col">
              <div>Your accounts if any, will be settled by our Finance Department.</div> <br>
              <div>
                Your contribution to the organization and its success will always be appreciated. We thank you for your services <br>
                and take this opportunity to wish you all the very best in your future career endeavors.
              </div>
            </div>
          </div> <br>
          <div class="row">
            <div>
              Warm Regards,
              <br>
              <b>For Entity Name.</b>
            </div>
          </div>
        </div>
      </div>
      <div class="flex flex-center">
        <q-btn color="secondary" label="DOWNLOAD AND SEND" @click="downloadPDF" />
      </div>
    </div>
  </q-page>
</template>

<script>
import axios from "axios";
import html2canvas from "html2canvas";
import jsPDF from "jspdf";
export default {
  data() {
    return {
      name: null,
      empcode: null,
      email: null,
      designation: null,
      joindate: null,
      resignationdate: null,
      enddate: null,
      location: null,
      showLetter: false,
      hideForm: true,
    };
  },
  methods: {
    sendEmail(imageData, name, empcode) {
      const sub = `Service Letter || ${this.name} || ${this.empcode}`;
      const msg = `Hi ${this.name}, 

Hope you are doing well.

Thanks for your contribution and & efforts throughout your tenure.

Hereby, we have attached your RL. All the best for your future endeavors.

Best regards,
[Entity Name]`;
      console.log(imageData);
      const formData = new FormData();
      formData.append("email", this.email);
      formData.append("imageData", imageData);
      formData.append("sub", sub);
      formData.append("msg", msg);

      axios.post("http://localhost:8080/expLetter/sendEmail", formData, {
        headers: {
          "Content-Type": "multipart/form-data",
        },
      })
        .then((res) => alert("Letter has been sent through email"))
        .catch((err) => console.log(err));
    },


    async addItems() {
      console.log("add method called");
      this.hideForm = false;
      this.showLetter = true;

      const data = {
        name: this.name,
        empcode: this.empcode,
        email: this.email,
        designation: this.designation,
        joindate: this.joindate,
        resignationdate: this.resignationdate,
        enddate: this.enddate,
        location: this.location
      };

      try {
        const response = await fetch('http://localhost:8080/expLetter/addData', {
          method: 'POST',
          headers: {
            'Content-Type': 'application/json',
          },
          body: JSON.stringify(data)
        });

        if (!response.ok) {
          alert("Failed to add data!!");
          throw new Error('Failed to add product. Server responded with ' + response.status);
        }

        const responseData = await response.json();
        console.log('Data added successfully:', responseData);
        //alert("Data Added Successfully!!");
        // window.location.reload();
      } catch (error) {
        console.error('Error while adding data:', error.message);
      }

    },


    async downloadPDF() {
      const pdf = new jsPDF();
      const ServiceLetter = document.getElementById("ServiceLetter");

      html2canvas(ServiceLetter).then((canvas) => {
        const imageData = canvas.toDataURL('image/png');
        const imgWidth = 210; // A4 width in mm
        const pageHeight = 297; // A4 height in mm
        const imgHeight = (canvas.height * imgWidth) / canvas.width;
        let heightLeft = imgHeight;

        const pdf = new jsPDF('p', 'mm', 'a4');
        let position = 0;

        pdf.addImage(imageData, 'PNG', 0, position, imgWidth, imgHeight);
        heightLeft -= pageHeight;

        while (heightLeft >= 0) {
          position = heightLeft - imgHeight;
          pdf.addPage();
          pdf.addImage(imageData, 'PNG', 0, position, imgWidth, imgHeight);
          heightLeft -= pageHeight;
        }

        pdf.save('ServiceLetter.pdf');
        this.sendEmail(imageData);
        // this.sendEmail(pdf.output('blob')); // You can send PDF via email
      });
    },
  },
};
</script>
<style>
@media only screen and (min-width: 768px)
{
  .mobwidth{
    min-width: 700px;
  }
}
</style>