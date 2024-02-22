package com.example.consumeanyplaceapis.controller;

import java.awt.PageAttributes.MediaType;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.web.bind.annotation.PostMapping;
import org.springframework.web.bind.annotation.RequestBody;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RestController;
import org.springframework.web.reactive.function.client.WebClient;

import com.example.consumeanyplaceapis.Body;

import reactor.core.publisher.Mono;

@RestController
public class AnyplaceController {
	@Autowired
	WebClient.Builder client;
	
	@PostMapping("/loginUser")
	public String getPoisData(@RequestBody Body params) {
		String baseurl = "https://ap.cs.ucy.ac.cy:44/api/navigation/route";
		
	String response = 	WebClient.create(baseurl).post()
		.accept(org.springframework.http.MediaType.APPLICATION_JSON).contentType(org.springframework.http.MediaType.APPLICATION_JSON)
		.body(Mono.just(params), Body.class)
		.retrieve()
		.bodyToMono(String.class).block();
		return response;
	}

}
