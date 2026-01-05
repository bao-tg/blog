# Introduction

After creating [[obsidian-kindle-vocab]], I planned to write a post to fully summarize my journey on building it, cause it's my **very first open-source project**, but it seems like I always lack of the excitation to write.

However, after putting it there for 6 months, it had gotten 89 downloads, 19 stars in github, and the very first contribution from community, modest numbers. But I still appreciate it, so let me celebrate this small win in the New Year with my readers by writing a blog about it.

I don't want to write this as a typical technical report, just recap my pure thought process when built it :D. If you're interested in the technical report, read [this](doc/CRPII_FinalReport.pdf)

## The project

Simply, the project is a plugin in Obisidian, allows the user to update the Vocabulary Builder in Kindle to their vault.

## What's Obsidian?

A note-taking app, similar to Notion, but I hate Notion, because of the numerous number of updating patches, and the latency when the Notion loads each of my notes. Moreover, typing Latex in Notion is probably one of the greatest punishments for me.

I use Obsidian cause it's fast (it stores all the note locally), and all the notes are Markdown file, highly suitable for typing Latex. Moreover, it allows the user to download many type of "plugins" developed by a great community of developers. 

One of the core plugin, is Graphview, here, you can see a Graphview of my vault. 

![[img/Graphview.png]]

## What's Kindle?

A reading machine, created by Amazon. Basically, it's quite similar to an Ipad mini, but it uses Eink screen instead of the commercial screen technology like LCD, OLED. And the Eink screen is better for your eyes compared to the mentioned screen tech. I tend to read on this machine instead of surfing the Internet with my phone before bed time. I bought it primarily to create reading habits and fix my sleep :D.

## Kindle Vocabulary Builders

One of the very cool features of Kindle is that, users are enabled to look up any words during the reading, and these words are stored in the **Vocabulary Builders**, with the context, where we searched that words. For example:

![[img/VocabBuilder.png]]

## My idea

There is another cool feature, all of the highlights that you made during the reading, all of them are stored in the a single text file. And there is a [Kindle Highlight Plugin](https://forum.obsidian.md/t/new-plugin-kindle-highlights/17740) in Obsidian to sync it to your vault. It means that, when you read a book, every highlight note, can be synced directly to your note taking system. I found that this idea is cool, and start to look for a way to sync the Vocabulary Builder to Obsidian vault, but there's no plugin like that. So I decided to build one.

# Building phase

## Analysis

### Finding a file

All of the highlight in the Kindle is stored in a single text file `My Clipping.txt`, and I know for sure, that the [Kindle Highlight Plugin](https://forum.obsidian.md/t/new-plugin-kindle-highlights/17740) some how extract the information from that file into multiple Markdown file. So, I start to look for a file that store the "Kindle Vocabulary Builder". Suprisingly, I found that all of the information in "Kindle Vocabulary Builder" is stored in a single `db` file, `vocab.db`, this can be found when we connect the Kindle with our PC, via Micro USB connection. 

### Inspect the file

I use [DB Browser for SQLite (DB4S)](https://sqlitebrowser.org/) for inspecting the file, and realize that all of the information, the `Context`, and the `Book Title`. Actually, they are stored in different table. My idea is writing a simple SQL query to query all of them

```sql
SELECT w.word, l.usage, bi.title
FROM LOOKUPS l
JOIN WORDS w ON l.word_key = w.id
JOIN BOOK_INFO bi ON l.book_key = bi.id
```

### The first problem: Dictionary

One of the crucial problem, is the "Dictionary", the key components, since it provides the definition for words. And the Dictionary provided by Amazon is [DRM-protected](https://www.google.com/url?sa=i&source=web&rct=j&url=https://www.locklizard.com/document-security-blog/amazon-drm-kindle/&ved=2ahUKEwiBmKbqzfORAxVphq8BHTnfAJIQ1fkOegQICxAC&opi=89978449&cd&psig=AOvVaw013nC5zS-2kTuVhYA5JdXi&ust=1767675313319000). At first, I tried to use [Calibre](https://www.google.com/url?sa=t&source=web&rct=j&opi=89978449&url=https://calibre-ebook.com/&ved=2ahUKEwjFirD8zfORAxXMdvUHHR9SGiQQFnoECCEQAQ&usg=AOvVaw2wA3NBTna-dIazLZySVE7Y) to de-DRM the dictionary. However, I soonly realize that this is forbidden, and my plugin can be penalized in the future. That's why I need another way.

At first, I tried to search some of the open-source vocabulary online, and found [Webster's dictionary](https://github.com/matthewreagan/WebstersEnglishDictionary). But I soonly realize that the vocabulary isn't good enough, since it doesn't contain some of the uncommon words, I need to due with the words form (I want for a single word, the dictionary shows all of the words form), and even, format the definition is exhausted, for example, some of the definition is in the form "1. (Bot.)  A circle of two or more leaves, flowers, or other organs, about the same part or joint of a stem. 2. (Zoöl.)  A volution, or turn, of the spire of a univalve shell. 3. (Spinning)  The fly of a spindle.". I don't want to just throw everything in the definition part for readers to read, I want to format it beautifully. 

That's why I search for another way. I found another opensource project [Wiktionary](https://www.wiktionary.org/). And they provide an API to retrieve the data in the website. And I can format the definition, words form easily. For example, you can take a look at my [wiktionay.csv](https://drive.google.com/file/d/1yyfdPqF0jJ7Y54PPgLq4_sS0SgJ8p537/view) file here, and try to compare it with [websters.csv](https://github.com/matthewreagan/WebstersEnglishDictionary) to see the difference.

### Obsidian's documentations

Obsidian has a very beginner-friendly [documentations](https://docs.obsidian.md/Home) for builders. I read some main documents to gain the overall architect of a plugin, and try to understand some of the key terminologies "Modal", "Command",.etc. And, obviously, I need to learn Typescript syntax, at that point, I only knew Python, and Java (And almost don't remember any Java's syntax). 

### Github's problem

And since we cannot update the dictionary file `csv` into github. Therefore, I ask the users directly upload their file into Obsidian, and upload the whole `db` file in it too. Sure, this will increase the Vault's size of users..., but I didn't know whether there was a better solution.

## Key features

###  Feature 1: Learned/Unlearned words

Listing all the information there, without any meaningful features, seem like not a good product. Therefore, I thought of a way to let the user interact with their own note, by marking words as `learned/unlearned`, and sort the displayed note through it. 

I do this by reading the UI components of Obsidian, and came up with the idea adding one more attribute `learned` to the `MAIN` table in `db` file. And reading the UI, and learn how the users interact with it, and how does it update the whole database is one of the interesting things I learned during the building of the project, I've never thought that the simple interaction has quite complex underlying software.

### Feature 2: Files' directory

Another feature that I want to add, is allow the user to update the directory of their files. I really, really want to let the user update the files' directory dynamically, by using the cursor and interacting directly with the file. However, it seems out of my ability at that time, the only way I thought of was building a "Settings Tab" that sepcify which directories the logic (update/store) will be performed. And I know, this is quite stupid idea, but I really hope that my readers can recommend me a way to improve, I am very open to hear a good solution/idea from you guys. And that's the beauty of an opensource project, isn't it?.

### Feature 3: Sorting words

In the `vocab.db`, there is a `TIMESTAMP` corresponding for each word. We can sort the information file in the Markdown file by using `ORDER` syntax in SQL. I also let the user sort words, based on "Unlearned first".

## My main idea

After carefully understand everything, I plug everything together. Write a code to extract Markdown file from SQL database, in Typescript, under Obsidian's documentations. And finish the project.

You can see the overall architect of the project here:

![[blockdiagram.png]]

A `vocab.db` will be retrieved from Kindle, alongside with the dictionary. It will create the `MAIN` table and the `vocab.db` database, these information aren't visible for users, only developers need to care about it. The users will receive the only Markdown file.

# Testing phase

I test each component, and their function manually, without writing any test program (Actually, I don't know how to do it...), And since the project is small, I honestly think there's no need to do that. Full testing phase can be found again in the [technical report](doc/CRPII_FinalReport.pdf)

Key thing I want to share is that, this is also the first time I learn how to debug in Console log :v, by printing stuff and open the `Ctrl + Shift + I` to check. Sound shameful for a senior CS student, I admit :D. 

# Submit to Obisidian's Plugins

I developed everything in only 2 weeks, and demonstrated successfully in the class, where I got 100/100 in every assignments for this project. However, after clean the code, and write the [documentation](obsidian-kindle-vocab.md), I started to submit to Obsidian's plugins on 26/05/2025.

Basically, first there will be a bot that will scan your code and ask for some minimal changes. I fixed everything and wait until 01/07/2025..., and closed and reopened the Pull Request for multiple times. Only on 23/07/2025, it turned out that there is a minor bug that I forgot to fix..., damn, I had waited for 2 months for nothing... This issue only was pointed out by a member (Discord name: `mnaoumov`) in Obisidian community...

And after that, this was the first time I know how bad I was at programming..., hardcode, putting https URL into the codebase,.etc. You can take a look at my [Pull Request](https://github.com/obsidianmd/obsidian-releases/pull/6510), to see the numerous feedback I received from the Obsidian's developer...

I learned a lot, thanks to both Obsidian community and developers. Only in 7/10/2025, my PR was updated into Obsidian store. It took me 2 weeks to build, but over than 4 months to wait, clean the code, and for the plugin to appear in Obsidian's plugin store.

# Conclusion

I want to add more features in the future, like a system that help users learn via spaced repetition, system that remind the users to study like Duolingo, a better Dictionary file, more dictionaries beside English,.etc. 

And since this is my first open-source project, I really hope to receive feedback, and contribution from community to learn how to organize file, how to manage a project at large scale.

The journey was harsh, but fun. My highschool version had never thought of the day I become a builder, ok, I admit that all I care about at that time was money. This project actually brought a new perspective for me about being an engineer, a builder.

I write everything on my own, no GPT, no spelling checker, no re-read :))). Hope you guys won't be too strict with me :D.