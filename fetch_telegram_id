package main

import (
	"encoding/json"
	"fmt"
	"io/ioutil"
	"log"
	"net/http"
)

type Update struct {
	Result []struct {
		Message struct {
			Chat struct {
				ID   int64  `json:"id"`
				Type string `json:"type"`
				Username string `json:"username,omitempty"`
				FirstName string `json:"first_name,omitempty"`
				LastName string `json:"last_name,omitempty"`
				Title string `json:"title,omitempty"`
			} `json:"chat"`
			Text string `json:"text"`
		} `json:"message"`
		ChannelPost struct {
			Chat struct {
				ID       int64  `json:"id"`
				Username string `json:"username"`
				Title    string `json:"title"`
			} `json:"chat"`
			Text string `json:"text"`
		} `json:"channel_post"`
	} `json:"result"`
}

const token = "YOUR_BOT_TOKEN"

func getUpdates() (*Update, error) {
	url := fmt.Sprintf("https://api.telegram.org/bot%s/getUpdates", token)
	resp, err := http.Get(url)
	if err != nil {
		return nil, err
	}
	defer resp.Body.Close()

	body, err := ioutil.ReadAll(resp.Body)
	if err != nil {
		return nil, err
	}

	var updates Update
	if err := json.Unmarshal(body, &updates); err != nil {
		return nil, err
	}

	return &updates, nil
}

func getUserChatID(updates *Update) {
	for _, update := range updates.Result {
		if update.Message.Chat.Type == "private" {
			fmt.Printf("User Chat ID: %d\n", update.Message.Chat.ID)
			fmt.Printf("Username: @%s\n", update.Message.Chat.Username)
			fmt.Printf("Name: %s %s\n", update.Message.Chat.FirstName, update.Message.Chat.LastName)
			return
		}
	}
	fmt.Println("No user messages found.")
}

func getGroupChatID(updates *Update) {
	for _, update := range updates.Result {
		if update.Message.Chat.Type == "group" || update.Message.Chat.Type == "supergroup" {
			fmt.Printf("Group Chat ID: %d\n", update.Message.Chat.ID)
			fmt.Printf("Group Name: %s\n", update.Message.Chat.Title)
			return
		}
	}
	fmt.Println("No group messages found.")
}

func getChannelChatID(updates *Update) {
	for _, update := range updates.Result {
		if update.ChannelPost.Chat.ID != 0 {
			fmt.Printf("Channel Chat ID: %d\n", update.ChannelPost.Chat.ID)
			fmt.Printf("Channel Username: @%s\n", update.ChannelPost.Chat.Username)
			fmt.Printf("Channel Title: %s\n", update.ChannelPost.Chat.Title)
			return
		}
	}
	fmt.Println("No channel posts found.")
}

func main() {
	updates, err := getUpdates()
	if err != nil {
		log.Fatal(err)
	}

	fmt.Println("Fetching User, Group, and Channel Chat IDs...")
	getUserChatID(updates)
	getGroupChatID(updates)
	getChannelChatID(updates)

	fmt.Println("\nFetching Complete!")
}
