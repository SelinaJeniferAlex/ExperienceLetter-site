<template>
    <q-page class="flex flex-center">
        <div style="max-width: 600px; margin: 20px auto">
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
                            <div>{{ issueDate }}</div> <br>
                            <div>Name: {{ name }}</div>
                            <div>Employee ID: {{ empcode }}</div>
                            <div>Location: {{ location }}</div>
                        </div>
                    </div>
                    <div class="flex flex-center q-ma-md">
                        <div style="text-align: center;">
                            <u><p>RELIEVING CUM SERVICE CERTIFICATE</p></u>
                        </div>
                    </div>
                    <div class="row">
                        <div>
                            <p>
                                With reference to your resignation dated <b>{{resignationdate}}</b>, we hereby accept your resignation from the
                                services of the company. Please note that you have been relieved from the services of the
                                company effective close of business hours on <b>{{enddate}}</b>.
                            </p>
                        </div>
                    </div>
                    <div class="row">
                        <div>
                            <div>Your service record with the Company is as follows:</div> <br>
                            <div>Date of Joining : {{joindate}}</div>
                            <div>Date of Leaving : {{enddate}}</div>
                            <div>Current Designation : {{designation}}</div>
                        </div>
                    </div> <br>
                    <div class="row">
                        <div>
                            <div>Your accounts if any, will be settled by our Finance Department.</div> <br>
                            <div>
                                Your contribution to the organization and its success will always be appreciated. We thank you
                                for your services and take this opportunity to wish you all the very best in your future career
                                endeavors.
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
        </div>
  </q-page>
</template>
<script>
import { defineComponent } from 'vue'

export default defineComponent({
  name: 'GenerateLetter'
})
</script>