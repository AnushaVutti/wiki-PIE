<h3>Kafka Producer--------------------------------------->Topic name</h3>
<br>
Company Profile Service-------------------------------------> _Company Detail_<br>
Company Profile Service------------------------------------->_Company Detail Add_<br>
User Profile Service   -------------------------------------> _User Detail_


<br><br>
<h3>Topic Name------------------------------------------->Kafka Consumer</h3>
<br>
_Company Detail_ ------------------------------------------->Company Authentication Service<br>
_User Detail_ ---------------------------------------------->User Authentication Service<br>
_Company Detail Add_---------------------------------------->Search Service<br>
_Company Detail Add_---------------------------------------->Recomandation Service<br>

<br><br>
<h3>Steps for kafka configurations:</h3>
* pom.xml : Add dependencies : <br>

`<dependency>`
            `<groupId>org.springframework.kafka</groupId>`
            `<artifactId>spring-kafka</artifactId>`
        `</dependency>`

`<dependency>`
            `<groupId>org.springframework.kafka</groupId>`
            `<artifactId>spring-kafka-test</artifactId>`
            `<scope>test</scope>`
        `</dependency>`


<br><br>
<h3>Producer Side settings</h3>
<br>
1=> Create one package with name "configuration" and add one configuration file "KafkaConfiguation.java" : <br>
<br>

package com.stackroute.pie.configuration;

import com.stackroute.pie.Model.User;
import org.apache.kafka.clients.producer.ProducerConfig;
import org.apache.kafka.common.serialization.StringSerializer;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;
import org.springframework.kafka.core.DefaultKafkaProducerFactory;
import org.springframework.kafka.core.KafkaTemplate;
import org.springframework.kafka.core.ProducerFactory;
import org.springframework.kafka.support.serializer.JsonSerializer;

import java.util.HashMap;
import java.util.Map;



@Configuration
public class KafkaConfiguration {

    @Bean
    public ProducerFactory<String, User> producerFactory() {
        Map<String, Object> config = new HashMap<>();

        config.put(ProducerConfig.BOOTSTRAP_SERVERS_CONFIG, "192.168.43.245:9092");
        config.put(ProducerConfig.KEY_SERIALIZER_CLASS_CONFIG, StringSerializer.class);
        config.put(ProducerConfig.VALUE_SERIALIZER_CLASS_CONFIG, JsonSerializer.class);
        System.out.println("inside producer factory*************************");
        return new DefaultKafkaProducerFactory<>(config);
    }


    @Bean
    public KafkaTemplate<String, User> kafkaTemplate() {
        return new KafkaTemplate<>(producerFactory());
    }


}
<br><br>
2=> use Kafka template to send json detail to kafka topic: 
<br>
<br>
(a)=> autowire kafka config file to controller: <br>
        @Autowired
        private KafkaTemplate<String, User> kafkaTemplate;
<br>
<br>
(b)=> Send jason detial to kafka topic using Kafka template:
<br>
<br>
kafkaTemplate.send("your topic name",user);

<br><br>
<h3>Consumer side settings:</h3>
<br>
(a)=> create one KafkaConfiguration.java file under configuation packege.

<br>
package com.techprimers.kafka.springbootkafkaconsumerexample.config;

import com.techprimers.kafka.springbootkafkaconsumerexample.model.User;
import com.techprimers.kafka.springbootkafkaconsumerexample.model.User1;
import org.apache.kafka.clients.consumer.ConsumerConfig;
import org.apache.kafka.common.serialization.StringDeserializer;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;
import org.springframework.kafka.annotation.EnableKafka;
import org.springframework.kafka.config.ConcurrentKafkaListenerContainerFactory;
import org.springframework.kafka.core.ConsumerFactory;
import org.springframework.kafka.core.DefaultKafkaConsumerFactory;
import org.springframework.kafka.support.serializer.JsonDeserializer;

import java.util.HashMap;
import java.util.Map;

@EnableKafka
@Configuration
public class KafkaConfiguration {

    @Bean
    public ConsumerFactory<String, String> consumerFactory() {
        Map<String, Object> config = new HashMap<>();

        config.put(ConsumerConfig.BOOTSTRAP_SERVERS_CONFIG, "192.168.43.245:9092");
        config.put(ConsumerConfig.GROUP_ID_CONFIG, "group_id");
        config.put(ConsumerConfig.KEY_DESERIALIZER_CLASS_CONFIG, StringDeserializer.class);
        config.put(ConsumerConfig.VALUE_DESERIALIZER_CLASS_CONFIG, StringDeserializer.class);
        System.out.println("Inside consumer factory------------");

        return new DefaultKafkaConsumerFactory<>(config);
    }


    @Bean
    public ConcurrentKafkaListenerContainerFactory<String, String> kafkaListenerContainerFactory() {
        ConcurrentKafkaListenerContainerFactory<String, String> factory = new ConcurrentKafkaListenerContainerFactory();
        factory.setConsumerFactory(consumerFactory());
        return factory;
    }


    @Bean
    public ConsumerFactory<String, User1> userConsumerFactory() {
        Map<String, Object> config = new HashMap<>();

        config.put(ConsumerConfig.BOOTSTRAP_SERVERS_CONFIG, "192.168.43.245:9092");
        config.put(ConsumerConfig.GROUP_ID_CONFIG, "group_json");
        config.put(ConsumerConfig.KEY_DESERIALIZER_CLASS_CONFIG, StringDeserializer.class);
        config.put(ConsumerConfig.VALUE_DESERIALIZER_CLASS_CONFIG, JsonDeserializer.class);
        System.out.println("Inside consumer factory json------------");
        return new DefaultKafkaConsumerFactory<>(config, new StringDeserializer(),
                new JsonDeserializer<>(User1.class));
    }

    @Bean
    public ConcurrentKafkaListenerContainerFactory<String, User1> userKafkaListenerFactory() {
        ConcurrentKafkaListenerContainerFactory<String, User1> factory = new ConcurrentKafkaListenerContainerFactory<>();
        factory.setConsumerFactory(userConsumerFactory());
        return factory;
    }

}
  
<br>
<br>

(b)=> Create KafkaConsumer.java file under listener packege
<br>
package com.techprimers.kafka.springbootkafkaconsumerexample.listener;

import com.techprimers.kafka.springbootkafkaconsumerexample.model.User;
import com.techprimers.kafka.springbootkafkaconsumerexample.model.User1;
import org.springframework.kafka.annotation.KafkaListener;
import org.springframework.stereotype.Service;

@Service
public class KafkaConsumer {

    @KafkaListener(topics = "your topic name (String datatype)", group = "group_id")
    public void consume(String message) {
        System.out.println("String wala method");
        System.out.println("Consumed message1: " + message);
    }



    @KafkaListener(topics = "deepak_json", group = "group_json", containerFactory = "userKafkaListenerFactory")
    public void consumeJson(User1 user) {
        System.out.println("yoyoyoyoyo");
        System.out.println("Consumed JSON Message: " + user);
    }
}



<br>
<br>


<h2>Note:</h2>
1.please use the same file stracture at consumer as present in producer other wise consumer will not be able to consume the Topic
<br><br>
2.use the same pojo file at consumer to get data from Kafka as producer have used to send the data to kafka topic(even the pojo file name should also be same).<br><br>
3.for any query contact <b>Deepak Patwa</b>
